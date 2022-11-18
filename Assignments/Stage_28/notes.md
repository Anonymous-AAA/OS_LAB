1. MAX_MEM_PAGE is set to 512 in spl constants
2. Placing locks in nexpos is important
3. The process will be set to CREATED State in the end of fork system to prevent it from getting scheduled by the other core.