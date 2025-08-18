---
layout: post
title: "Tổng hợp kiến thức về Spring MVC (Web Layer)"
date: 2025-07-05
---

1.  Kiến trúc MVC

            |------------------------------------------------------------------|
            | Thành phần | Vai trò                                             |
            |------------------------------------------------------------------|
            | Model      | Chứa dữ liệu (DTO, Entity)                          |
            | View       | Giao diện người dùng (Thymeleaf, JSP...)            |
            | Controller | Xử lý logic điều hướng, nhận request – trả response |

2.  @Controller, @RestController, @RequestMapping, @GetMapping, @PostMapping, @PathVariable, @RequestParam, @RequestBody, @ResponseBody

            |----------------------------------------------------------------------------------------------------------------|
            | Annotation      | Chức năng                                    | Dùng khi                                      |
            |----------------------------------------------------------------------------------------------------------------|
            | @Controller     | Đánh dấu 1 class là controller               | web truyền thống (trả về HTML)                |
            | @RestController | = @Controller + @ResponseBody, trả JSON/XML  | REST API                                      |
            | @RequestMapping | Ánh xạ path chung cho controller hoặc method | Cho method/class                              |
            | @GetMapping     | GET request                                  | Dùng cho api trả về dữ liệu                   |
            | @PostMapping    | POST request                                 | Dùng cho api tạo dữ liệu                      |
            | @PutMapping     | PUT request                                  | Dùng cho api cập nhật toàn bộ một resource    |
            | @PatchMapping   | PATCH request                                  | Dùng cho api cập nhật một phần của resource |
            | @DeleteMapping  | DELETE request                               | dùng cho api xóa một resource                 |
            | @PathVariable   | Lấy dữ liệu từ URL path                      | /users/{id}                                   |
            | @RequestParam   | Lấy query param (?key=value)                 | ?keyword=abc                                  |
            | @RequestBody    | Map JSON body vào Java object                | Dùng với POST, PUT                            |
            | @ResponseBody   | Trả object dưới dạng JSON                    | Nếu không dùng @RestController                |

    - Ví dụ:

           {% raw %}
           @RestController
           @RequestMapping("/users")
           public class UserController {

            @GetMapping("/{id}")
            public UserDto getUser(@PathVariable Long id) {
              return userService.getUser(id);
            }

            @PostMapping
            public ResponseEntity<?> createUser(@RequestBody @Valid UserDto userDto) {
              userService.create(userDto);
              return ResponseEntity.ok("Created");
            }
           }
           {% endraw %}

3.  Binding dữ liệu: DTO, Form object

        - DTO: Data Transfer Object – trung gian giữa request và service
        - Form object: DTO dùng để binding dữ liệu từ form (hoặc JSON)
        - Ví dụ:

               {% raw %}
               public class UserDto {
               @NotBlank
               private String name;

               @Email
               private String email;
               }
               {% endraw %}

           | Spring tự map JSON → object thông qua @RequestBody.

4.  Exception handling: @ControllerAdvice, @ExceptionHandler

    a. Tạo custom handler toàn cục

                       {% raw %}
                       @ControllerAdvice
                       public class GlobalExceptionHandler {

                        @ExceptionHandler(EntityNotFoundException.class)
                        public ResponseEntity<String> handleNotFound(EntityNotFoundException ex) {
                          return ResponseEntity.status(HttpStatus.NOT_FOUND).body(ex.getMessage());
                        }

                        @ExceptionHandler(MethodArgumentNotValidException.class)
                        public ResponseEntity<?> handleValidation(MethodArgumentNotValidException ex) {
                          Map<String, String> errors = new HashMap<>();
                          ex.getBindingResult().getFieldErrors()
                            .forEach(err -> errors.put(err.getField(), err.getDefaultMessage()));
                          return ResponseEntity.badRequest().body(errors);
                        }
                       }
                       {% endraw %}

    b. Custom exception:

                       {% raw %}
                       public class EntityNotFoundException extends RuntimeException {
                        public EntityNotFoundException(String message) {
                        super(message);
                        }
                       }
                       {% endraw %}

5.  Validations: @Valid, @Validated, Bean Validation API (JSR-303)

            |--------------------------------------------------------------------------------------------------|
            | Annotation                       | Ý nghĩa                                                       |
            |--------------------------------------------------------------------------------------------------|
            | @Valid                           | Kiểm tra đối tượng theo rule validation (thường dùng cho DTO) |
            | @Validated                       | Giống @Valid nhưng hỗ trợ Group                               |
            | @NotNull, @Size, @Min, @Email... | Các ràng buộc có sẵn từ Bean Validation API                   |

    - Ví dụ:

                       {% raw %}
                       @PostMapping
                       public ResponseEntity<?> createUser(@RequestBody @Valid UserDto userDto) {
                        // Nếu sai -> MethodArgumentNotValidException
                        userService.save(userDto);
                        return ResponseEntity.ok("Success");
                       }
                       {% endraw %}

             | Chúng ta cần thêm spring-boot-starter-validation để dùng được @Valid.
