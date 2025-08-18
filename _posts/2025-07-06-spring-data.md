---
layout: post
title: "Tổng hợp kiến thức về Spring Data JPA / Spring JDBC"
date: 2025-07-06
---

1.  ORM là gì?

    - ORM (Object Relational Mapping) là kỹ thuật ánh xạ giữa object trong Java và bảng trong CSDL.

      - Mỗi class Java ↔ một bảng trong DB
      - Mỗi field ↔ một cột
      - Mỗi instance ↔ một dòng dữ liệu

    Mục đích: giúp truy vấn DB bằng Java object, không cần viết SQL thủ công nhiều.

2.  Spring Data JPA với JpaRepository, CrudRepository, PagingAndSortingRepository

    a. Spring Data JPA là gì?

    - Spring Data JPA là một abstraction trên JPA giúp tự động sinh code truy vấn CRUD.
    - Nó tích hợp với JPA Provider như Hibernate.

    b. Các interface chính trong Spring Data JPA

            |-------------------------------------------------------------------------------------------------------------|
            | Interface                         | Chức năng                                                               |
            |-------------------------------------------------------------------------------------------------------------|
            | CrudRepository<T, ID>             | Cung cấp các hàm CRUD cơ bản (save, findById, delete...)                |
            | PagingAndSortingRepository<T, ID> | Thêm hỗ trợ phân trang & sắp xếp                                        |
            | JpaRepository<T, ID>              | Kế thừa tất cả trên + nhiều tính năng mở rộng như batch, flush, khóa... |

    - Ví dụ:

            {% raw %}
             public interface UserRepository extends JpaRepository<User, Long> {
               List<User> findByName(String name);
             }
            {% endraw %}

3.  Viết custom query bằng JPQL, native SQL, hoặc @Query

    a. Query Method:

           {% raw %}
            List<User> findByEmailAndStatus(String email, String status);
           {% endraw %}

    b. JPQL - Java Persistence Query Language(@Query):

           {% raw %}
            @Query("SELECT u FROM User u WHERE u.email = :email")
            User findByEmail(@Param("email") String email);
           {% endraw %}

    c. JPQL (@Query):

           {% raw %}
            @Query(value = "SELECT * FROM users WHERE email = ?1", nativeQuery = true)
            User findByEmailNative(String email);
           {% endraw %}

4.  Transaction management với @Transactional

    - Giúp đảm bảo thao tác DB là toàn vẹn (ACID).
    - Nếu có lỗi xảy ra, sẽ rollback toàn bộ.
    - Ví dụ:

           {% raw %}
            @Transactional
            public void transferMoney() {
              withdraw();
              deposit();
            }
           {% endraw %}

    - Mặc định @Transactional chỉ áp dụng trên public method.
    - Có thể cấu hình rollback, propagation, isolation...

5.  Entity Lifecycle (Persist, Merge, Remove, Detach)

            |---------------------------------------------------------------------------|
            | Trạng thái           | Mô tả                                              |
            |---------------------------------------------------------------------------|
            | New (Transient)      | Entity mới tạo, chưa được persist                  |
            | Managed (Persistent) | Entity được quản lý bởi EntityManager              |
            | Detached             | Entity đã từng persist nhưng giờ không còn quản lý |
            | Removed              | Entity sẽ bị xoá khỏi DB                           |

    - Các method liên quan:
      - persist(entity) – thêm mới
      - merge(entity) – cập nhật
      - remove(entity) – xoá
      - detach(entity) – tách khỏi context

6.  Cách tạo các mối quan hệ: OneToOne, OneToMany, ManyToOne, ManyToMany

                    |-------------------------------------------------------------------------------|
                    | Annotation   | Mối quan hệ | Ghi chú                                          |
                    |-------------------------------------------------------------------------------|
                    | @OneToOne    |  1 - 1      | Một đối tượng liên kết với đúng 1 đối tượng khác |
                    | @OneToMany   |  1 - N      | Một đối tượng có nhiều đối tượng con             |
                    | @ManyToOne   |  N - 1      | N đối tượng con trỏ về cùng 1 đối tượng cha      |
                    | @ManyToMany  |  N - N      | N đối tượng liên kết với N đối tượng khác        |

    a. Ví dụ @OneToOne – Một-một (Một User có một Profile):

                   {% raw %}
                    @Entity
                    public class User {
                      @Id @GeneratedValue
                      private Long id;
                      private String username;

                      @OneToOne(mappedBy = "user", cascade = CascadeType.ALL)
                      private Profile profile;
                    }

                    @Entity
                    public class Profile {
                      @Id @GeneratedValue
                      private Long id;
                      private String bio;

                      @OneToOne
                      @JoinColumn(name = "user_id")
                      private User user;
                    }
                   {% endraw %}

    - Giải thích:
      - @OneToOne(mappedBy = "user"): quan hệ được điều khiển bởi Profile
      - @JoinColumn(name = "user_id"): khoá ngoại

    b. Ví dụ @OneToMany - Một-Nhiều (Một Customer có nhiều Order) và @ManyToOne - Nhiều-Một (Nhiều Order có chung một Customer)

                   {% raw %}
                    @Entity
                    public class Customer {
                      @Id @GeneratedValue
                      private Long id;
                      private String name;

                      @OneToMany(mappedBy = "customer", cascade = CascadeType.ALL)
                      private List<Order> orders = new ArrayList<>();
                    }

                    @Entity
                    public class Order {
                      @Id @GeneratedValue
                      private Long id;
                      private String orderCode;

                      @ManyToOne
                      @JoinColumn(name = "customer_id")
                      private Customer customer;
                    }
                   {% endraw %}

    - Giải thích:
      - Order là bên sở hữu quan hệ, chứa @JoinColumn
      - Customer là bên không sở hữu, dùng mappedBy = "customer"
    - Thêm đơn hàng:

                  {% raw %}
                   Customer c = new Customer();
                   Order o1 = new Order(); o1.setCustomer(c);
                   Order o2 = new Order(); o2.setCustomer(c);
                   c.setOrders(List.of(o1, o2));
                   customerRepository.save(c); // cascade ALL nên tự lưu luôn orders
                  {% endraw %}

    c. Ví dụ @ManyToMany – Nhiều-nhiều (Student học nhiều Course, Course có nhiều Student)

                  {% raw %}
                  @Entity
                  public class Student {
                    @Id @GeneratedValue
                    private Long id;
                    private String name;

                    @ManyToMany
                    @JoinTable(name = "student_course",
                      joinColumns = @JoinColumn(name = "student_id"),
                      inverseJoinColumns = @JoinColumn(name = "course_id"))
                    private Set<Course> courses = new HashSet<>();
                  }

                  @Entity
                  public class Course {
                    @Id @GeneratedValue
                    private Long id;
                    private String title;

                    @ManyToMany(mappedBy = "courses")
                    private Set<Student> students = new HashSet<>();
                  }
                  {% endraw %}

    - Giải thích:

      - @JoinTable tạo bảng trung gian student_course
      - mappedBy = "courses" để định nghĩa quan hệ 2 chiều

    - Gán khóa học cho sinh viên:

                  {% raw %}
                  Student s = new Student();
                  Course c1 = new Course(); c1.setTitle("Java");
                  Course c2 = new Course(); c2.setTitle("Spring");

                  s.getCourses().addAll(List.of(c1, c2));
                  c1.getStudents().add(s);
                  c2.getStudents().add(s);
                  studentRepository.save(s); // sẽ lưu tất cả do cascade
                  {% endraw %}

7.  Lazy vs Eager Loading

            |----------------------------------------------------------------------------------------------------|
            | Kiểu   | Mô tả                                  | Ưu/nhược                                         |
            |----------------------------------------------------------------------------------------------------|
            | LAZY   | Chỉ load khi cần (lazy initialization) | Tốt hơn về hiệu năng nếu không cần dữ liệu ngay  |
            | EAGER  | Load luôn khi entity được lấy          | Gây N+1 query, giảm performance                  |

    - Ví dụ:

           {% raw %}
           @OneToMany(fetch = FetchType.LAZY)
           private List<Order> orders;
           {% endraw %}
