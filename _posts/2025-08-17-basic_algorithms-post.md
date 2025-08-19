---
layout: post
title: "Ôn tập kiến thức về thuật toán cơ bản"
date: 2025-08-17
---

**I. Khái niệm nền tảng**

- Thuật toán (Algorithm): tập hợp hữu hạn các bước để giải quyết một vấn đề.
- Độ phức tạp:
  - Time Complexity: thời gian chạy (O(1), O(log n), O(n), O(n log n), O(n²) …).
  - Space Complexity: bộ nhớ sử dụng.
  - Big-O notation: ký hiệu để biểu diễn độ phức tạp thuật toán theo input size n.

**II. Thuật toán tìm kiếm (Searching)**

**1. Linear Search (tuần tự)**

- Khi dùng: mảng/list nhỏ hoặc chưa sắp xếp.
- Độ phức tạp: O(n); bộ nhớ O(1)
- Ý tưởng: duyệt từ trái qua phải, gặp là trả về
  Ví dụ: [4, 2, 9, 7] tìm 9 → duyệt 4→2→9 (trả về index 2).

**2. Binary Search (nhị phân)**

- Khi dùng: mảng đã sắp xếp (rất quan trọng).
- Độ phức tạp: O(log n); bộ nhớ O(1).
- Ý tưởng: so sánh ở giữa, loại nửa không cần, lặp lại.
- Lưu ý biên: vòng lặp while (l <= r), mid = l + (r - l) / 2 để tránh tràn.
  Ví dụ: [1,3,5,7,9] tìm 7 → mid=5 < 7 ⇒ xét nửa phải → mid=7 (tìm thấy).

        {% raw %}
        public static int binarySearch(int[] a, int target) {
          int l = 0; // biên trái
          int r = a.length - 1; // biên phải

            while (l <= r) {
                int mid = l + (r - l) / 2; // tránh tràn số
                if (a[mid] == target) {
                    return mid; // tìm thấy, trả về index
                }
                if (a[mid] < target) {
                    l = mid + 1; // bỏ qua nửa trái
                } else {
                    r = mid - 1; // bỏ qua nửa phải
                }
            }
            return -1; // không tìm thấy
        }
       {% endraw %}

**II. Thuật toán tìm kiếm (Searching)**

**1. Bubble Sort**

- Ý tưởng:

  - Duyệt nhiều lần qua mảng.
  - Mỗi lần duyệt, so sánh cặp phần tử liền kề, nếu sai thứ tự thì hoán đổi.
  - Sau mỗi lượt, phần tử lớn nhất “nổi” lên cuối.

- Độ phức tạp:

  - Trung bình / Tệ nhất: O(n²)
  - Tốt nhất (mảng đã sort): O(n)
  - Bộ nhớ: O(1), ổn định.

- Ví dụ:

  - Mảng: [5, 1, 4, 2]
  - Lượt 1: (5,1) → swap → [1,5,4,2]; (5,4) → [1,4,5,2]; (5,2) → [1,4,2,5]
  - Lượt 2: (1,4), ok; (4,2) → [1,2,4,5]; (4,5) ok
    → Mảng đã sort.

        {% raw %}
        public static void bubbleSort(int[] a) {
          boolean swapped;
          int n = a.length;
          do {
              swapped = false;
              for (int i = 1; i < n; i++) {
                  if (a[i - 1] > a[i]) {
                      int tmp = a[i];
                      a[i] = a[i - 1];
                      a[i - 1] = tmp;
                      swapped = true;
                  }
              }
              n--; // phần tử cuối đã đúng vị trí
          } while (swapped);
        }
        {% endraw %}

**2. Selection Sort**

- Ý tưởng:

  - Ở mỗi vòng lặp, tìm phần tử nhỏ nhất trong đoạn chưa sort, đưa nó về đầu.
  - Sau vòng thứ i, các phần tử [0..i] đã đúng chỗ.

- Độ phức tạp:

  - Trung bình / Tệ nhất: O(n²)
  - Không ổn định, bộ nhớ O(1).

- Ví dụ:

  - Mảng [29, 10, 14, 37]
  - Lượt 1: min=10 → swap với 29 → [10,29,14,37]
  - Lượt 2: min=14 → swap với 29 → [10,14,29,37] → Done.

        {% raw %}
        public static void selectionSort(int[] a) {
            int n = a.length;
            for (int i = 0; i < n - 1; i++) {
                int min = i;
                for (int j = i + 1; j < n; j++) {
                    if (a[j] < a[min]) min = j;
                }
                int tmp = a[i];
                a[i] = a[min];
                a[min] = tmp;
            }
        }
        {% endraw %}

**3. Insertion Sort**

- Ý tưởng:

  - Duyệt từ trái sang phải.
  - Với mỗi phần tử, chèn nó vào đúng vị trí trong đoạn đã sort trước đó.

- Độ phức tạp:

  - Trung bình / Tệ nhất: O(n²)
  - Tốt nhất (mảng gần như sort): O(n)
  - Ổn định, bộ nhớ O(1).

- Ví dụ:

  - Mảng [5, 3, 4]
  - 5: đoạn đã sort [5].
  - 3: chèn vào trước 5 → [3,5].
  - 4: chèn giữa 3 và 5 → [3,4,5].

        {% raw %}
        public static void insertionSort(int[] a) {
            for (int i = 1; i < a.length; i++) {
                int key = a[i];
                int j = i - 1;
                while (j >= 0 && a[j] > key) {
                    a[j + 1] = a[j];
                    j--;
                }
                a[j + 1] = key;
            }
        }
        {% endraw %}

**4. Merge Sort**

- Ý tưởng:

  - Chia để trị:

    - Chia mảng thành 2 nửa.
    - Sắp xếp từng nửa đệ quy.
    - Gộp (merge) 2 nửa đã sort.

- Độ phức tạp:

  - Luôn O(n log n)
  - Bộ nhớ: O(n), ổn định.

- Ví dụ:

  - Mảng [38, 27, 43, 3]
  - Chia: [38,27] và [43,3].
  - Sort trái → [27,38]; sort phải → [3,43].
  - Merge → [3,27,38,43].

        {% raw %}
        public static void mergeSort(int[] a) {
            if (a.length <= 1) return;
            int[] tmp = new int[a.length];
            mergeSort(a, 0, a.length - 1, tmp);
        }

        private static void mergeSort(int[] a, int l, int r, int[] tmp) {
            if (l >= r) return;
            int m = l + (r - l) / 2;
            mergeSort(a, l, m, tmp);
            mergeSort(a, m + 1, r, tmp);
            merge(a, l, m, r, tmp);
        }

        private static void merge(int[] a, int l, int m, int r, int[] tmp) {
            int i = l, j = m + 1, k = l;
            while (i <= m && j <= r) {
                if (a[i] <= a[j]) tmp[k++] = a[i++];
                else tmp[k++] = a[j++];
            }
            while (i <= m) tmp[k++] = a[i++];
            while (j <= r) tmp[k++] = a[j++];
            for (int t = l; t <= r; t++) a[t] = tmp[t];
        }
        {% endraw %}

**5. Quick Sort (chia để trị)**

- Ý tưởng:

  - Chia để trị:

    1. Chọn pivot (thường là giữa, trái, phải hoặc ngẫu nhiên).
    2. Phân chia mảng thành 2 phần: ≤ pivot và ≥ pivot.
    3. Đệ quy sort 2 nửa.

- Độ phức tạp:

  - Trung bình: O(n log n)
  - Tệ nhất: O(n²) (pivot xấu).
  - Bộ nhớ: O(log n), không ổn định.

- Ví dụ:

  - Mảng [9,3,7,1], pivot=7
  - Nhỏ hơn pivot: [3,1], lớn hơn: [9].
  - Sort [3,1] → [1,3].
  - Merge lại: [1,3,7,9].

        {% raw %}
        public static void quickSort(int[] a) {
            quickSort(a, 0, a.length - 1);
        }

        private static void quickSort(int[] a, int l, int r) {
            if (l >= r) return;
            int pivot = a[l + (r - l) / 2];
            int i = l, j = r;
            while (i <= j) {
                while (a[i] < pivot) i++;
                while (a[j] > pivot) j--;
                if (i <= j) {
                    int tmp = a[i]; a[i] = a[j]; a[j] = tmp;
                    i++; j--;
                }
            }
            if (l < j) quickSort(a, l, j);
            if (i < r) quickSort(a, i, r);
        }
        {% endraw %}

**6. Heap Sort**

- Ý tưởng:

  - Xây max-heap từ mảng.
  - Lặp: swap root (max) với phần tử cuối, giảm heap-size, heapify lại.

- Độ phức tạp:

  - Luôn O(n log n)
  - In-place, không ổn định.

- Ví dụ:

  - Mảng [4,10,3,5,1]
  - Heapify → [10,5,3,4,1]
  - Swap 10 ↔ 1 → [1,5,3,4,10]
  - Heapify → [5,4,3,1,10]
  - Swap 5 ↔ 1 → [1,4,3,5,10]
    → v.v.

        {% raw %}
        public static void heapSort(int[] a) {
            int n = a.length;
            for (int i = n / 2 - 1; i >= 0; i--) heapify(a, n, i);
            for (int end = n - 1; end > 0; end--) {
                int tmp = a[0]; a[0] = a[end]; a[end] = tmp;
                heapify(a, end, 0);
            }
        }

        private static void heapify(int[] a, int n, int i) {
            int largest = i, left = 2*i + 1, right = 2*i + 2;
            if (left < n && a[left] > a[largest]) largest = left;
            if (right < n && a[right] > a[largest]) largest = right;
            if (largest != i) {
                int tmp = a[i]; a[i] = a[largest]; a[largest] = tmp;
                heapify(a, n, largest);
            }
        }
        {% endraw %}

**7. Counting Sort**

- Ý tưởng:
  - Đếm tần suất xuất hiện của từng số trong [min..max].
  - Tính prefix sum để biết vị trí.
  - Sắp xếp ổn định bằng cách chèn ngược.
- Độ phức tạp:
  - O(n + k), k = phạm vi giá trị.
  - Bộ nhớ O(n+k), ổn định.

**8. Radix Sort (áp dụng cho dữ liệu số nguyên lớn)**

- Ý tưởng:
  - Sort theo từng chữ số (hàng đơn vị → chục → trăm).
  - Dùng Counting Sort ổn định ở mỗi bước.
- Độ phức tạp:
  - O(d·(n + b)), với d = số chữ số, b = cơ số (10).
  - Ổn định, tốt cho số nguyên lớn, không âm.
