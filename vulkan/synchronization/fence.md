# Бар'єр
Примітив синхронізації, який реалізується з допомогою операційної системи. Бар'єри даються командам, котрі взаємодіють з операційною системою, таким як vkQueueSubmit(). Коли робота цих команд завершується, бар'єр взводиться (сигналізує).  
Оскільки бар'єр часто відповідає "рідному" примітиву синхронізації для операційної системи, то потоки можуть засипати до моменту сигналу бар'єру. Враховуючи останнє, цей примітив повинен використовуватись в операціях, які можуть мати певний час для завершення. Наприклад, завершення виконання командних буферів чи показу завершеного кадру користувачу.

    VkResult vkCreateFence(
	      VkDevice device,  
		  const VkFenceCreateInfo* pCreateInfo, 
		  const VkAllocationCallbacks* pAllocator, 
		  VkFence* pFence
	); 
	
    void vkDestroyFence(
	      VkDevice device,
		  VkFence  fence,
		  const VkAllocationCallbacks* pAllocator
	);  

Программа користувача може в будь-який момент перевірити стан бар'єру:  

    VkResult vkGetFenceStatus(VkDevice device, VkFence fence);  

У випадку успіху, функція верне одне з двух значень:  
- VK_SUCCESS бар'єр в данний момент взведений  
- VK_NOT_READY бар'єр в данний момент не взведений  
Якщо була якась помилка з отриманням статусу бар'єру, то функція верне код помилки.  
Для того щоб очікувати завершення бар'єру, необхідно викликати функцію:   

    vkWaitForFences(
	    VkDevice device,
		uint32_t fenceCount,
		const VkFence* pFences,
		VkBool32 waitAll,
		uint64_t timeout
	);    















