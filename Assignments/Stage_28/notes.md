1. MAX_MEM_PAGE is set to 512 in spl constants
2. Placing locks in nexpos is important
3. The process will be set to CREATED State in the end of fork system to prevent it from getting scheduled by the other core.
4. Made changes in scheduler to Schedule the Shell process if  LOGOUT_STATUS=1 and the secondary core is  running IDLE2.