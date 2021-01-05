#title
Linux: How flexible are the min requirements?

#body
Hello, I'm a web & mobile developer, but not a gamer; so I don't aim for systems with high end graphics cards or pay much attention to hardware beside Disk, RAM, & CPU performance rank. I saw some courses for UE4 & got excited about it.  I didn't really note any system requirements in the requirements section, so I bought them and got straight to cloning & building UE4.  I went through all the steps and everything on the CLI seemed good, but it crashes with a 'signal 11' when I try to launch.

I found a few posts here and there. One mentioned adding a ppa & updating the system, 
`apt-add-repository ppa:oibaf/graphics-drivers && apt-get update && apt-get dist-upgrade`
I ran that, but still get the errors mentioned below.

I read through more wiki pages about installing on Linux and noted the section emphasizing Ubuntu & the minimum system requirements. [here](https://ue4community.wiki/legacy/building-on-linux-qr8t0si2)
> Quad-core Intel or AMD processor, 2.5 GHz or faster
> NVIDIA GeForce 470 GTX or AMD Radeon 6870 HD series card or higher
> 8 GB RAM
But see various posts mentioning other distros, graphics cards, etc, and hope that suggest that maybe this is just a minimum for a 'guaranteed win.'

I am using a new HP Envy x360 that I bought a few months ago & have setup Pop OS 20.10 on.  
Checking the specs I have:
> Intel® Core™ i7-10510U CPU @ 1.80GHz × 8
> Mesa Intel® UHD Graphics (CML GT2)

I saw a post that mentioned they had luck launching with an `--openGL4` flag on the CLI, but that didn't seem to do anything.  There is no man page installed to look at and `--help` & `--options` only launched UE4 so I'm not sure it even takes args. I am not finding much more, so now I am here.

Any help is greatly appreciated.
Todd


I get these details when the crash reporter opens:
```
    LoginId:xxxxxxxxxxxxxxxx
    EpicAccountId:

    Fatal error: [File:/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/VulkanRHI/Private/VulkanUtil.cpp] [Line: 803] VulkanRHI::vkQueueSubmit(Queue, 1, &SubmitInfo, Fence->GetHandle()) failed, VkResult=-4 at /home/logos/Dev/UnrealEngine/Engine/Source/Runtime/VulkanRHI/Private/VulkanQueue.cpp:71 with error VK_ERROR_DEVICE_LOST 0x00007ff303c3817f libUE4Editor-VulkanRHI.so!VulkanRHI::VerifyVulkanResult(VkResult, char const*, char const*, unsigned int) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/VulkanRHI/Private/VulkanUtil.cpp:802] 0x00007ff303c0f4b8 libUE4Editor-VulkanRHI.so!FVulkanQueue::Submit(FVulkanCmdBuffer*, unsigned int, VkSemaphore_T**) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/VulkanRHI/Private/VulkanQueue.cpp:71] 0x00007ff303ba7b9a libUE4Editor-VulkanRHI.so!FVulkanCommandBufferManager::SubmitUploadCmdBuffer(unsigned int, VkSemaphore_T**) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/VulkanRHI/Private/VulkanCommandBuffer.cpp:547] 0x00007ff303c70411 libUE4Editor-VulkanRHI.so!FVulkanSurface::InternalLockWrite(FVulkanCommandListContext&, FVulkanSurface*, VkImageSubresourceRange const&, VkBufferImageCopy const&, VulkanRHI::FStagingBuffer*) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/VulkanRHI/Private/VulkanTexture.cpp:170] 0x00007ff303c79477 libUE4Editor-VulkanRHI.so!FRHICommand<FRHICommandLockWriteTexture, FUnnamedRhiCommand>::ExecuteAndDestruct(FRHICommandListBase&, FRHICommandListDebugContext&) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/RHI/Public/RHICommandList.h:763] 0x00007ff387b4e62e libUE4Editor-RHI.so!FRHICommandListExecutor::ExecuteInner_DoExecute(FRHICommandListBase&) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/RHI/Private/RHICommandList.cpp:373] 0x00007ff387bce196 libUE4Editor-RHI.so!FExecuteRHIThreadTask::DoTask(ENamedThreads::Type, TRefCountPtr<FGraphEvent> const&) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/RHI/Private/RHICommandList.cpp:428] 0x00007ff387bcd802 libUE4Editor-RHI.so!TGraphTask<FExecuteRHIThreadTask>::ExecuteTask(TArray<FBaseGraphTask*, TSizedDefaultAllocator<32> >&, ENamedThreads::Type) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/Core/Public/Async/TaskGraphInterfaces.h:886] 0x00007ff38d39b27c libUE4Editor-Core.so!FNamedTaskThread::ProcessTasksNamedThread(int, bool) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/Core/Private/Async/TaskGraph.cpp:709] 0x00007ff38d39997e libUE4Editor-Core.so!FNamedTaskThread::ProcessTasksUntilQuit(int) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/Core/Private/Async/TaskGraph.cpp:600] 0x00007ff387d8aebd libUE4Editor-RenderCore.so!FRHIThread::Run() [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/RenderCore/Private/RenderingThread.cpp:319] 0x00007ff38d44b127 libUE4Editor-Core.so!FRunnableThreadPThread::Run() [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/Core/Private/HAL/PThreadRunnableThread.cpp:25] 0x00007ff38d40f4f3 libUE4Editor-Core.so!FRunnableThreadPThread::_ThreadProc(void*) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/Core/Private/HAL/PThreadRunnableThread.h:185] 0x00007ff38dd90590 libpthread.so.0!UnknownFunction(0x958f) 0x00007ff384757223 libc.so.6!clone(+0x42)

    libUE4Editor-Core.so!FGenericPlatformMisc::RaiseException(unsigned int) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/Core/Private/GenericPlatform/GenericPlatformMisc.cpp:472]
    libUE4Editor-Core.so!FOutputDevice::LogfImpl(char16_t const*, ...) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/Core/Private/Misc/OutputDevice.cpp:61]
    libUE4Editor-VulkanRHI.so!VulkanRHI::VerifyVulkanResult(VkResult, char const*, char const*, unsigned int) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/VulkanRHI/Private/VulkanUtil.cpp:802]
    libUE4Editor-VulkanRHI.so!FVulkanQueue::Submit(FVulkanCmdBuffer*, unsigned int, VkSemaphore_T**) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/VulkanRHI/Private/VulkanQueue.cpp:71]
    libUE4Editor-VulkanRHI.so!FVulkanCommandBufferManager::SubmitUploadCmdBuffer(unsigned int, VkSemaphore_T**) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/VulkanRHI/Private/VulkanCommandBuffer.cpp:547]
    libUE4Editor-VulkanRHI.so!FVulkanSurface::InternalLockWrite(FVulkanCommandListContext&, FVulkanSurface*, VkImageSubresourceRange const&, VkBufferImageCopy const&, VulkanRHI::FStagingBuffer*) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/VulkanRHI/Private/VulkanTexture.cpp:170]
    libUE4Editor-VulkanRHI.so!FRHICommand<FRHICommandLockWriteTexture, FUnnamedRhiCommand>::ExecuteAndDestruct(FRHICommandListBase&, FRHICommandListDebugContext&) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/RHI/Public/RHICommandList.h:763]
    libUE4Editor-RHI.so!FRHICommandListExecutor::ExecuteInner_DoExecute(FRHICommandListBase&) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/RHI/Private/RHICommandList.cpp:373]
    libUE4Editor-RHI.so!FExecuteRHIThreadTask::DoTask(ENamedThreads::Type, TRefCountPtr<FGraphEvent> const&) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/RHI/Private/RHICommandList.cpp:428]
    libUE4Editor-RHI.so!TGraphTask<FExecuteRHIThreadTask>::ExecuteTask(TArray<FBaseGraphTask*, TSizedDefaultAllocator<32> >&, ENamedThreads::Type) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/Core/Public/Async/TaskGraphInterfaces.h:886]
    libUE4Editor-Core.so!FNamedTaskThread::ProcessTasksNamedThread(int, bool) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/Core/Private/Async/TaskGraph.cpp:709]
    libUE4Editor-Core.so!FNamedTaskThread::ProcessTasksUntilQuit(int) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/Core/Private/Async/TaskGraph.cpp:600]
    libUE4Editor-RenderCore.so!FRHIThread::Run() [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/RenderCore/Private/RenderingThread.cpp:319]
    libUE4Editor-Core.so!FRunnableThreadPThread::Run() [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/Core/Private/HAL/PThreadRunnableThread.cpp:25]
    libUE4Editor-Core.so!FRunnableThreadPThread::_ThreadProc(void*) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/Core/Private/HAL/PThreadRunnableThread.h:185]
    libpthread.so.0!UnknownFunction(0x958f)
    libc.so.6!clone(+0x42)
```
    

 I see these logs from the log file that look like the start of the error below.
```
    [2021.01.02-06.36.21:290][  0]LogSlate: Took 0.000158 seconds to synchronously load lazily loaded font '../../../Engine/Content/Slate/Fonts/Roboto-Bold.ttf' (160K)
    [2021.01.02-06.36.21:496][  0]LogShaderCompilers: Display: Worker (2/5): shaders left to compile 3413
    [2021.01.02-06.36.22:121][  0]LogVulkanRHI: Error: VulkanRHI::vkQueueSubmit(Queue, 1, &SubmitInfo, Fence->GetHandle()) failed, VkResult=-4
        at /home/logos/Dev/UnrealEngine/Engine/Source/Runtime/VulkanRHI/Private/VulkanQueue.cpp:71 
        with error VK_ERROR_DEVICE_LOST
    [2021.01.02-06.36.22:125][  0]LogCore: Error: appError called: Fatal error: [File:/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/VulkanRHI/Private/VulkanUtil.cpp] [Line: 803] 
    VulkanRHI::vkQueueSubmit(Queue, 1, &SubmitInfo, Fence->GetHandle()) failed, VkResult=-4
        at /home/logos/Dev/UnrealEngine/Engine/Source/Runtime/VulkanRHI/Private/VulkanQueue.cpp:71 
        with error VK_ERROR_DEVICE_LOST
    0x00007f285f9d317f libUE4Editor-VulkanRHI.so!VulkanRHI::VerifyVulkanResult(VkResult, char const*, char const*, unsigned int) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/VulkanRHI/Private/VulkanUtil.cpp:802]
    0x00007f285f9aa4b8 libUE4Editor-VulkanRHI.so!FVulkanQueue::Submit(FVulkanCmdBuffer*, unsigned int, VkSemaphore_T**) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/VulkanRHI/Private/VulkanQueue.cpp:71]
    0x00007f285f942b9a libUE4Editor-VulkanRHI.so!FVulkanCommandBufferManager::SubmitUploadCmdBuffer(unsigned int, VkSemaphore_T**) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/VulkanRHI/Private/VulkanCommandBuffer.cpp:547]
    0x00007f285fa0b411 libUE4Editor-VulkanRHI.so!FVulkanSurface::InternalLockWrite(FVulkanCommandListContext&, FVulkanSurface*, VkImageSubresourceRange const&, VkBufferImageCopy const&, VulkanRHI::FStagingBuffer*) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/VulkanRHI/Private/VulkanTexture.cpp:170]
    0x00007f285fa14477 libUE4Editor-VulkanRHI.so!FRHICommand<FRHICommandLockWriteTexture, FUnnamedRhiCommand>::ExecuteAndDestruct(FRHICommandListBase&, FRHICommandListDebugContext&) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/RHI/Public/RHICommandList.h:763]
    0x00007f28e376e62e libUE4Editor-RHI.so!FRHICommandListExecutor::ExecuteInner_DoExecute(FRHICommandListBase&) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/RHI/Private/RHICommandList.cpp:373]
    0x00007f28e37ee196 libUE4Editor-RHI.so!FExecuteRHIThreadTask::DoTask(ENamedThreads::Type, TRefCountPtr<FGraphEvent> const&) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/RHI/Private/RHICommandList.cpp:428]
    0x00007f28e37ed802 libUE4Editor-RHI.so!TGraphTask<FExecuteRHIThreadTask>::ExecuteTask(TArray<FBaseGraphTask*, TSizedDefaultAllocator<32> >&, ENamedThreads::Type) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/Core/Public/Async/TaskGraphInterfaces.h:886]
    0x00007f28e8fbb27c libUE4Editor-Core.so!FNamedTaskThread::ProcessTasksNamedThread(int, bool) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/Core/Private/Async/TaskGraph.cpp:709]
    0x00007f28e8fb997e libUE4Editor-Core.so!FNamedTaskThread::ProcessTasksUntilQuit(int) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/Core/Private/Async/TaskGraph.cpp:600]
    0x00007f28e39aaebd libUE4Editor-RenderCore.so!FRHIThread::Run() [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/RenderCore/Private/RenderingThread.cpp:319]
    0x00007f28e906b127 libUE4Editor-Core.so!FRunnableThreadPThread::Run() [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/Core/Private/HAL/PThreadRunnableThread.cpp:25]
    0x00007f28e902f4f3 libUE4Editor-Core.so!FRunnableThreadPThread::_ThreadProc(void*) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/Core/Private/HAL/PThreadRunnableThread.h:185]
    0x00007f28e99b0590 libpthread.so.0!UnknownFunction(0x958f)
    0x00007f28e0377223 libc.so.6!clone(+0x42)

    [2021.01.02-06.36.22:141][  0]LogCore: === Critical error: ===
    Unhandled Exception: SIGSEGV: invalid attempt to write memory at address 0x0000000000000003

    [2021.01.02-06.36.22:141][  0]LogCore: Fatal error: [File:/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/VulkanRHI/Private/VulkanUtil.cpp] [Line: 803] 
    VulkanRHI::vkQueueSubmit(Queue, 1, &SubmitInfo, Fence->GetHandle()) failed, VkResult=-4
        at /home/logos/Dev/UnrealEngine/Engine/Source/Runtime/VulkanRHI/Private/VulkanQueue.cpp:71 
        with error VK_ERROR_DEVICE_LOST
    0x00007f285f9d317f libUE4Editor-VulkanRHI.so!VulkanRHI::VerifyVulkanResult(VkResult, char const*, char const*, unsigned int) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/VulkanRHI/Private/VulkanUtil.cpp:802]
    0x00007f285f9aa4b8 libUE4Editor-VulkanRHI.so!FVulkanQueue::Submit(FVulkanCmdBuffer*, unsigned int, VkSemaphore_T**) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/VulkanRHI/Private/VulkanQueue.cpp:71]
    0x00007f285f942b9a libUE4Editor-VulkanRHI.so!FVulkanCommandBufferManager::SubmitUploadCmdBuffer(unsigned int, VkSemaphore_T**) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/VulkanRHI/Private/VulkanCommandBuffer.cpp:547]
    0x00007f285fa0b411 libUE4Editor-VulkanRHI.so!FVulkanSurface::InternalLockWrite(FVulkanCommandListContext&, FVulkanSurface*, VkImageSubresourceRange const&, VkBufferImageCopy const&, VulkanRHI::FStagingBuffer*) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/VulkanRHI/Private/VulkanTexture.cpp:170]
    0x00007f285fa14477 libUE4Editor-VulkanRHI.so!FRHICommand<FRHICommandLockWriteTexture, FUnnamedRhiCommand>::ExecuteAndDestruct(FRHICommandListBase&, FRHICommandListDebugContext&) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/RHI/Public/RHICommandList.h:763]
    0x00007f28e376e62e libUE4Editor-RHI.so!FRHICommandListExecutor::ExecuteInner_DoExecute(FRHICommandListBase&) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/RHI/Private/RHICommandList.cpp:373]
    0x00007f28e37ee196 libUE4Editor-RHI.so!FExecuteRHIThreadTask::DoTask(ENamedThreads::Type, TRefCountPtr<FGraphEvent> const&) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/RHI/Private/RHICommandList.cpp:428]
    0x00007f28e37ed802 libUE4Editor-RHI.so!TGraphTask<FExecuteRHIThreadTask>::ExecuteTask(TArray<FBaseGraphTask*, TSizedDefaultAllocator<32> >&, ENamedThreads::Type) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/Core/Public/Async/TaskGraphInterfaces.h:886]
    0x00007f28e8fbb27c libUE4Editor-Core.so!FNamedTaskThread::ProcessTasksNamedThread(int, bool) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/Core/Private/Async/TaskGraph.cpp:709]
    0x00007f28e8fb997e libUE4Editor-Core.so!FNamedTaskThread::ProcessTasksUntilQuit(int) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/Core/Private/Async/TaskGraph.cpp:600]
    0x00007f28e39aaebd libUE4Editor-RenderCore.so!FRHIThread::Run() [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/RenderCore/Private/RenderingThread.cpp:319]
    0x00007f28e906b127 libUE4Editor-Core.so!FRunnableThreadPThread::Run() [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/Core/Private/HAL/PThreadRunnableThread.cpp:25]
    0x00007f28e902f4f3 libUE4Editor-Core.so!FRunnableThreadPThread::_ThreadProc(void*) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/Core/Private/HAL/PThreadRunnableThread.h:185]
    0x00007f28e99b0590 libpthread.so.0!UnknownFunction(0x958f)
    0x00007f28e0377223 libc.so.6!clone(+0x42)

    0x00007f28e8fe7bfe libUE4Editor-Core.so!FGenericPlatformMisc::RaiseException(unsigned int) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/Core/Private/GenericPlatform/GenericPlatformMisc.cpp:472]
    0x00007f28e9232c1b libUE4Editor-Core.so!FOutputDevice::LogfImpl(char16_t const*, ...) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/Core/Private/Misc/OutputDevice.cpp:61]
    0x00007f285f9d317f libUE4Editor-VulkanRHI.so!VulkanRHI::VerifyVulkanResult(VkResult, char const*, char const*, unsigned int) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/VulkanRHI/Private/VulkanUtil.cpp:802]
    0x00007f285f9aa4b8 libUE4Editor-VulkanRHI.so!FVulkanQueue::Submit(FVulkanCmdBuffer*, unsigned int, VkSemaphore_T**) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/VulkanRHI/Private/VulkanQueue.cpp:71]
    0x00007f285f942b9a libUE4Editor-VulkanRHI.so!FVulkanCommandBufferManager::SubmitUploadCmdBuffer(unsigned int, VkSemaphore_T**) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/VulkanRHI/Private/VulkanCommandBuffer.cpp:547]
    0x00007f285fa0b411 libUE4Editor-VulkanRHI.so!FVulkanSurface::InternalLockWrite(FVulkanCommandListContext&, FVulkanSurface*, VkImageSubresourceRange const&, VkBufferImageCopy const&, VulkanRHI::FStagingBuffer*) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/VulkanRHI/Private/VulkanTexture.cpp:170]
    0x00007f285fa14477 libUE4Editor-VulkanRHI.so!FRHICommand<FRHICommandLockWriteTexture, FUnnamedRhiCommand>::ExecuteAndDestruct(FRHICommandListBase&, FRHICommandListDebugContext&) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/RHI/Public/RHICommandList.h:763]
    0x00007f28e376e62e libUE4Editor-RHI.so!FRHICommandListExecutor::ExecuteInner_DoExecute(FRHICommandListBase&) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/RHI/Private/RHICommandList.cpp:373]
    0x00007f28e37ee196 libUE4Editor-RHI.so!FExecuteRHIThreadTask::DoTask(ENamedThreads::Type, TRefCountPtr<FGraphEvent> const&) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/RHI/Private/RHICommandList.cpp:428]
    0x00007f28e37ed802 libUE4Editor-RHI.so!TGraphTask<FExecuteRHIThreadTask>::ExecuteTask(TArray<FBaseGraphTask*, TSizedDefaultAllocator<32> >&, ENamedThreads::Type) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/Core/Public/Async/TaskGraphInterfaces.h:886]
    0x00007f28e8fbb27c libUE4Editor-Core.so!FNamedTaskThread::ProcessTasksNamedThread(int, bool) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/Core/Private/Async/TaskGraph.cpp:709]
    0x00007f28e8fb997e libUE4Editor-Core.so!FNamedTaskThread::ProcessTasksUntilQuit(int) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/Core/Private/Async/TaskGraph.cpp:600]
    0x00007f28e39aaebd libUE4Editor-RenderCore.so!FRHIThread::Run() [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/RenderCore/Private/RenderingThread.cpp:319]
    0x00007f28e906b127 libUE4Editor-Core.so!FRunnableThreadPThread::Run() [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/Core/Private/HAL/PThreadRunnableThread.cpp:25]
    0x00007f28e902f4f3 libUE4Editor-Core.so!FRunnableThreadPThread::_ThreadProc(void*) [/home/logos/Dev/UnrealEngine/Engine/Source/Runtime/Core/Private/HAL/PThreadRunnableThread.h:185]
    0x00007f28e99b0590 libpthread.so.0!UnknownFunction(0x958f)
    0x00007f28e0377223 libc.so.6!clone(+0x42)

    [2021.01.02-06.36.22:143][  0]LogExit: Executing StaticShutdownAfterError
```






