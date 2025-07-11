# 排序算法实践（一）：冒泡、选择与插入排序

---

### 1. 核心内容 (Core Content)

排序是计算机科学中最基本、最核心的操作之一。本章将介绍三种最基础的、时间复杂度为 O(n²) 的排序算法：冒泡排序、选择排序和插入排序。虽然它们的效率不高，不常用于大规模数据的生产环境，但其思想简单直观，是理解更高级排序算法（如快速排序、归并排序）的重要基石。

**核心知识点：**
- **冒泡排序 (Bubble Sort)**:
    - **思想**: 重复地遍历待排序的序列，一次比较两个相邻的元素，如果它们的顺序错误就把它们交换过来。这个过程就像气泡从水底冒到水面一样。
    - **特点**: 每轮遍历后，最大的元素会“沉”到序列的末尾。
    - **优化**: 如果在一轮遍历中没有发生任何交换，说明序列已经有序，可以提前终止算法。
- **选择排序 (Selection Sort)**:
    - **思想**: 首先在未排序序列中找到最小（大）元素，存放到排序序列的起始位置，然后再从剩余未排序元素中继续寻找最小（大）元素，然后放到已排序序列的末尾。
    - **特点**: 每次都选择一个“最值”放到正确的位置。交换次数少，但不稳定。
- **插入排序 (Insertion Sort)**:
    - **思想**: 构建有序序列，对于未排序数据，在已排序序列中从后向前扫描，找到相应位置并插入。就像打扑克牌时，将新摸到的牌插入到手中已有序的牌里。
    - **特点**: 对于部分有序的数组，效率很高。稳定。

---

### 2. 学习目标 (Learning Objectives)

- **深刻理解冒泡排序、选择排序和插入排序的核心思想和执行过程。**
- **能够使用 Python 从零开始实现这三种排序算法。**
- **能够分析并说出这三种算法的时间复杂度（均为 O(n²)）和空间复杂度（均为 O(1)）。**
- **理解算法的“稳定性”概念，并能判断这三种排序是否稳定。**
- **了解冒泡排序的优化方法（提前终止）。**

---

### 3. 价值与目的 (Purpose and Value)

- **建立排序算法基础**: 这三种算法是入门排序世界的最佳途径，为学习更高效的 O(n log n) 算法打下坚实的基础。
- **锻炼编程基本功**: 实现这些算法需要熟练运用循环、判断和数组/列表操作，是很好的编程练习。
- **理解时空权衡**: 虽然时间复杂度相同，但它们在交换次数、比较次数等方面有细微差别，有助于理解算法分析的细节。
- **面试入门题**: 在面试中可能会被要求手写这些简单排序，以考察候选人的基本功是否扎实。

---

### 4. 高级技巧与注意事项 (Advanced Techniques & Pitfalls)

- **算法稳定性 (Stability)**:
    - **定义**: 如果待排序的序列中存在值相等的元素，经过排序后，这些相等元素的相对位置不发生改变，则该排序算法是稳定的。
    - **判断**:
        - 冒泡排序：稳定（因为只交换相邻元素）。
        - 插入排序：稳定（因为是逐个移动找到插入位置）。
        - 选择排序：不稳定（因为找到的最小元素会与前面的元素交换，可能打乱相等元素的顺序）。
- **适用场景**:
    - 这三种算法都不适合大规模数据排序。
    - **插入排序**在数据量小或数据基本有序的情况下，性能表现非常好，甚至优于快速排序等高级算法。因此，很多高级排序算法（如 TimSort，Python 内置排序）在处理小规模子数组时会切换到插入排序。
- **Python 实现细节**: Python 的赋值语句 `a, b = b, a` 可以非常方便地交换两个变量的值，无需临时变量。

---

### 5. 蓝图计划与代码示例 (Blueprint & Code Examples)

#### 冒泡排序 (Bubble Sort)

```python
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        # 优化：如果一轮没有交换，则已排好序
        swapped = False
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True
        if not swapped:
            break
    return arr
```

#### 选择排序 (Selection Sort)

```python
def selection_sort(arr):
    n = len(arr)
    for i in range(n):
        min_idx = i
        for j in range(i + 1, n):
            if arr[j] < arr[min_idx]:
                min_idx = j
        # 将找到的最小元素与第 i 个位置的元素交换
        arr[i], arr[min_idx] = arr[min_idx], arr[i]
    return arr
```

#### 插入排序 (Insertion Sort)

```python
def insertion_sort(arr):
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1
        # 将比 key 大的元素向后移动
        while j >= 0 and key < arr[j]:
            arr[j + 1] = arr[j]
            j -= 1
        # 插入 key
        arr[j + 1] = key
    return arr
```

---

### 6. 推荐资源 (Recommended Resources)

-   **书籍**: 《算法图解》 - 对这些排序算法有非常生动的图解。
-   **可视化网站**:
    -   [VisuAlgo](https://visualgo.net/en/sorting) - 动态展示排序过程。
    -   [Sorting.at](https://sorting.at/) - 提供多种排序算法的可视化和声音效果。
-   **LeetCode**: [912. 排序数组](https://leetcode-cn.com/problems/sort-an-array/) - 可以用这个题目来测试自己实现的各种排序算法。
