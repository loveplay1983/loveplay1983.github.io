---
title: "PyTorch device - GPU - CPU"
date: 2025-02-02 15:32:00 +0800
categories: [Data Science]
tags: [AI Tools]
---

In PyTorch, specifying the device for computations is crucial for leveraging hardware accelerators like GPUs. 

1. ```python
   device = torch.device('cuda' if torch.cuda.is_available() else 'cpu')
   ```

2. ```python
   gpu_indx = 0
   device = torch.device(f"cuda:{gpu_indx}" if torch.cuda.is_available() else "cpu")
   ```

**Key Differences:**

- **Default GPU Selection:**
  - In the first snippet, `torch.device('cuda')` selects the current CUDA device, which defaults to GPU 0 unless changed elsewhere in the code.
  - In the second snippet, `torch.device(f"cuda:{gpu_indx}")` explicitly specifies GPU 0 (since `gpu_indx` is set to 0).

- **Flexibility:**
  - The first approach is straightforward and suitable when we intend to use the default GPU.
  - The second approach offers flexibility, allowing us to set `gpu_indx` to any available GPU index, which is beneficial in multi-GPU systems.

**Considerations:**

- **Multi-GPU Systems:**
  - If the system has multiple GPUs and we want to utilize a specific one, the second approach is preferable. By changing the value of `gpu_indx`, we can direct PyTorch to use a particular GPU.

- **Consistency:**
  - Ensure that the rest of the code consistently uses the `device` variable to move models and tensors to the correct device. For example:
    ```python
    model.to(device)
    tensor = tensor.to(device)
    ```

In summary, both approaches aim to set the computing device for PyTorch operations. The first is concise and defaults to GPU 0 when available, while the second provides explicit control over which GPU to use, making it more suitable for scenarios involving multiple GPUs. 