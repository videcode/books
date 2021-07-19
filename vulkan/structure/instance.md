# Instance  
```c  
VkResult vkCreateInstance (  
    const VkInstanceCreateInfo* pCreateInfo,  
	const VkAllocationCallbacks* pAllocator,  
	VkInstance* pInstance  
);  

typedef struct VkInstanceCreateInfo {  
  VkStructureType sType;  
  const void* pNext;  
  VkInstanceCreateFlags flags;
  const VkApplicationInfo* pApplicationInfo;
  uint32_t enabledLayrCount;
  const char* const* ppEnabledLayerNames;
  uint32_t enabledExtensionCount;
  const char* const* ppEnabledExtensionNames;
} VkInstanceCreateInfo;  

typedef struct VkApplicationInfo {
  VkStructureType sType;
  const void* pNext;
  const char* pApplicationName;
  uint32_t applicationVersion;
  const char* pEngineName;
  uint32_t engineVersion;
  uint32_t apiVersion;
} VkApplicationInfo;
```  
