# Physical device  
```c
VkResult vkEnumeratePhysicalDevices (
  VkInstance instance,
  uint32_t* pPhysicalDeviceCount,
  VkPhysicalDevice* pPhysicalDevices
);
```
 Якщо pPhysicalDevices дорівнює nullptr,то функція верне в pPhysicalDeviceCount кількість пристроїв. Інакше параметр pPhysicalDeviceCount вказує на кількість пристроїв котрі потрібно вернути. 

```c
void vkGetPhysicalDeviceProperties (
  VkPhysicalDevice physicalDevice,
  VkPhysicalDeviceProperties* pProperties
);

typedef struct VkPhysicalDeviceProperties {
  uint32_t apiVersion;
  uint32_t driverVersion;
  uint32_t vendorID;
  uint32_t deviceID;
  VkPhysicalDeviceType deviceType;
  char deviceName[VK_MAX_PHYSICAL_DEVICE_NAME_SIZE];
  uint8_t pipelineCacheUUID[VK_UUID_SIZE];
  VkPhysicalDeviceLimits limits;
  VkPhysicalDeviceProperties sparseProperties;
} VkPhysicalDeviceProperties;

void vkGetPhysicalDeviceFeatures (
  VkPhysicalDevice physicalDevice,
  VkPhysicalDeviceFeatures* pFeatures
);
```

##### Пам'ять
 Пам'ять пристрою котра доступна йому та може бути використана для зберігання текстур та інших данних. Пам'ть ділиться на типи, кожен з котрих має певний набір властивостей, таких як флаги кешування та когерентність між пристроем та CPU. Кожномутипу пам'яті відповідає одна з куч(heap) пристрою, яких може бути декілька.
```c
void vkGetPhysicalDeviceMemoryProperties (
  VkPhysicalDevice physicalDevice,
  VkPhysicalDeviceMemoryProperties* pMemoryProperties
);

typedef struct VkPhysicalDeviceMemoryProperties {
  uint32_t memoryTypeCount;
  VkMemoryType memoryTypes[VK_MAX_MEMORY_TYPES];
  uint32_t memoryHeapCount;
  VkMemoryHeap memoryHeaps[VK_MAX_MEMORY_HEAPS];
} VkPhysicalDeviceMemoryProperties;

typedef struct VkMemoryType{
  VkMemoryPropertyFlags propertyFlags;
  uint32_t heapIndex;
} VkMemoryType;
```
Поле propertyFlags структури VkMemoryType вміщує набір флагів:  
- **VK_MEMORY_PROPERTY_DEVICE_LOCAL_BIT** пам'ять являється локальною для пристрою (фізично під'єднання до нього). Якщо цей біт не встановленний, то пам'ять рахується локальною по відношенню до CPU.
- **VK_MEMORY_PROPERTY_HOST_VISIBLE_BIT** память цього типу можу бути відображенна та зчитуватись чи записуватись CPU. Якщо цей тип не встановленний, то пам'ять цього типу не може бути напряму доступна CPU та предназначенна скоріше виключно для пристрою.
- **VK_MEMORY_PROPERTY_HOST_COHERENT_BIT** цей біт означає, шо коли відбувається одночасне звернення до пам'яті пристроєм та CPU, то ці звернення будуть узгодженні (когерентні) між ними. Якщо цей біт не встановленнний, то CPU чи GPU можуть не побачити результати записів до тих пір, поки кеші явно не скинуті.
- **VK_MEMORY_PROPERTY_HOST_CACHED_BIT** означає, що данні цього типу пам'яті кешуються на стороні CPU. Читання з цього типу пам'яті зазвичай буде бистріше ніж якщо цей біт не був би  встановленний. Однак доступ зі сторони GPU може мати вищу латентність, особливо якщо пам'ять когерентна.
- **VK_MEMORY_PROPERTY_LAZILIY_ALLOCATED_BIT** означає, що виділенна пам'ять данного типу не одразу займає місце у відповідній кучі і драйвер може відложити виділення фізичної пам'яті до моменту, коли ця пам'ять буде використана для якого-небудь ресурсу.
```c
typedef struct VkMemoryHeap {
  VkDeviceSize size;
  VkMemoryHeapFlags flags;
} VkMemoryHeap;
```
VkMemoryHeapFlags описує кучу. В vulkan 1.0 єдиним флагом є VK_MEMORY_HEAP_DEVICE_LOCAL_BIT, який вказує на те що куча являється локальною для пристрою. Це повністю відповідає аналогічному флагу для типів пам'яті.

