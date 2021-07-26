# Queue
Черга - це частина пристрою, що виконує завдання. Черги групуються сім'ями. Сім'я черги - це группа черг, що мають спільні властивості, але виконуються паралельно. Кількість сімей, їх властивості та кількисть черг в сім'ях встановлюється пристроєм.
```c
void vkGetPhysicalDeviceQueueFamilyProperties (
  VkPhysicalDevice physicalDevice,
  uint32_t* pQueueFamilyPropertyCount,
  VkQueueFamilyProperties* pQueueFamilyProperties
);

typedef struct VkQueueFamilyProperties{
  VkQueueFlags queueFlags;
  uint32_t queueCount;
  uint32_t timestampValidBits;
  VkExtent3D minImageTransferGranularity;
} VkQueueFamilyProperties;
```
queueFlags складається з комбінації бітів VkQueueFlagsBits:  
- **VK_QUEUE_GRAPHICS_BIT** якщо цей біт виставленний, то черги в цьому сімействі підтримують графічні операції, такі як рендеринг точок, відрізків та трикутників.
- **VK_QUEUE_COMPUTE_BIT** якщо цей виставленний, то черги в цій сім'ї підтримують обчислювальні операції, такі як запуск обчислювальних шейдерів.
- **VK_QUEUE_TRANSFER_BIT** черги підтримують операції копіювання, такі як копіювання контенту буферу та зображень.
- **VK_QUEUE_SPARSE_BINDING_BIT** черги підтримують операції прив'язування (binding) пам'яті для праці з розрідженними ресурсами.
