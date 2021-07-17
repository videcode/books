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
VkResult vkSetEvent(
    VkDevice device,
	VkEvent event
);
```  









