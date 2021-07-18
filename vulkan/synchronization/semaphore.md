# Семафор
Примітив синхронізації який представляє собою флаг, який може бути взведенний або зброшенний атомарно пристроєм. Семафори неможуть явно взводитись и скидуватись пристроем. Замість цього вони взводяться та очікують за допомогою операцій з чергами, такими як vkQueueSubmit().  
```c  
VkResult vkCreateSemaphore (  
    VkDevice device,  
	const VkSemaphoreCreateInfo* pCreateInfo,  
	const VkAllocationCallbacks* pAllocator,  
	VkSemaphore* pSemaphore  
);  

typedef struct VkSemaphoreCreateInfo {  
    VkStructureType sType;  
	const void* pNext;  
	VkSemaphoreCreateFlags flags; // зарезервованно і повинно = 0   
}  

void vkDestroySemaphore (  
    VkDevice device,  
	VkSemaphore semaphore,  
	const VkAllocationCallbacks* pAllocator  
);  
```  
