# Подія
Механізм точної синхронізації, який може використовуватись для обережного розділення операцій в конвеєрі. Стан події може керуватись як CPU так і приладом (але не у всіх місцях).  
Має два стани:  
- взведенний  
- невзведенний  

Оскільки не тільки CPU, а і прилад може міняти стан подій, то він може таким чином синхронізувати різні частини одного і того ж конвеєра.
Створення події:  
```c
VkResult vkCreateEvent(  
    VkDevice device,  
	const VkEventCreateInfo* pCreateInfo,  
	const VkAllocationCallbacks* pAllocator,  
	VkEvent* pEvent  
  );  

typedef struct VkEventCreateInfo {  
    VkStructureType sType;  
	const void* pNext;  
	VkEventCreateFlags flags;  
} VkEventCreateInfo;
```  
Поки що поле VkEventCreateFlags зарезервовано і повинно дорівнювати 0.  
Знищення події:  
```c  
void vkDestroyEvent(
    VkDevice device,
	VkEvent event,
	const VkAllocationCallbacks* pAlocator
);  
```  
Змінити стан зі сторони CPU:  
```c  
// взведенний  
VkResult vkSetEvent(
    VkDevice device,
	VkEvent event
);
// незведенний стан  
VkResult vkResetEvent(  
    VkDevice device,  
	VkEvent event  
);  
// перевірити стан  
VkResult vkGetEventStatus(  
    VkDevice device,  
	VkEvent event  
);  
// VK_EVENT_SET: взведенний стан  
// VK_EVENT_RESET: невзведенний стан  
```  
Доступ до події повинен бути зовні синхронізованний. Щоб CPU отримав сповіщення про зміну статусу потрібно в циклі чи іншим методом перевіряти vkGetEventStatus, бо інакшого варіанту немає.  

Події можуть керуватись пристроєм через командний буфер:  
```c  
void vkCmdSetEvent(  
    VkCommandBuffer commandBuffer,  
	VkEvent event,  
	VkPipelineStageFlags stageMask
);  

void vkCmdResetEvent(  
    VkCommandBuffer commandBuffer,  
	VkEvent event,  
	VkPipelineStageFlags stageMask
);  

void vkCmdWaitEvents (  
    VkCommandBuffer commandBuffer,  
	uint32_t eventCount,  
	const VkEvent* pEvents,  
	VkPipelineStageFlags srcStageMask,  
	VkPipelineStageFlags dstStageMask,  
	uint32_t memoryBarriers,  
	const VkMemoryBarrier* pMemoryBarriers,  
	uint32_t bufferMemoryBarrierCount,  
	const VkBufferMemoryBarrier* pBufferMemoryBarriers,  
	uint32_t imageMemoryBarrierCount,  
	const VkImageMemoryBarrier* pImageMemoryBarriers  
);  
```   
Коли один потік міняє стан події на взведенний, то якщо інший потік очікує цю подію з допомогою виклику vkCmdWaitEvents(), він негайно буде розблокованний.  








