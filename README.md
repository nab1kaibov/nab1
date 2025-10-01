Алиев уибо-12-24
Куча — это структура данных в виде бинарного дерева, где узел всегда имеет высший (макс-куча) или низший (мин-куча) приоритет относительно своих потомков. На практике её хранят в массиве: для элемента i его потомки находятся на позициях 2i+1 и 2i+2. Это обеспечивает эффективные операции (вставка и удаление за O(log n), доступ к корню — за O(1)).

В Python для мин-кучи используется модуль heapq:

heapq.heapify(list) — преобразует список в кучу.

heapq.heappush(heap, x) — добавляет элемент.

heapq.heappop(heap) — извлекает минимальный элемент.

Для макс-кучи значения инвертируют. Собственную реализацию (например, для операции decrease_key) создают на основе методов _sift_up и _sift_down.

Более сложные кучи (биномиальная, Фибоначчи) эффективны для слияния и операций decrease_key, но в стандартной библиотеке Python отсутствуют.

Хеш-таблица — это контейнер «ключ-значение», где хеш-функция преобразует ключ в индекс массива, обеспечивая в среднем O(1) для основных операций. В Python для этого используется dict.

Простая учебная реализация с методом цепочек:
class HashTable:
    def __init__(self, size=16):
        self.size = size
        self.table = [[] for _ in range(size)]  # Цепочки для коллизий

    def _hash(self, key):
        return hash(key) % self.size  # Простое хеширование

    def put(self, key, value):
        idx = self._hash(key)
        for i, (k, v) in enumerate(self.table[idx]):
            if k == key:
                self.table[idx][i] = (key, value)  # Обновление
                return
        self.table[idx].append((key, value))  # Вставка

    def get(self, key):
        idx = self._hash(key)
        for k, v in self.table[idx]:
            if k == key:
                return v
        raise KeyError(key)
