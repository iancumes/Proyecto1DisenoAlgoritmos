# Diagrama de Transición de Estados
Este diagrama muestra el flujo general de la máquina. Un paso a la derecha copia los valores y avanza la construcción hasta que se consumen todos los `1`s.

```mermaid
stateDiagram-v2
    direction TB
    [*] --> q0 : Start (Tape = 1^n)
    
    q0 --> q_accept : n=0 (empty tape)
    q0 --> init_find_end : read 1
    
    init_find_end --> init_write_hash2 : read _
    init_write_hash2 --> init_write_0 : read _
    init_write_0 --> rewind : write 0
    
    rewind --> rewind : move left over computed data
    rewind --> find_1 : hit _ at left end
    
    find_1 --> goto_end_for_hash : found next 1
    goto_end_for_hash --> find_B1_start : write trailing #
    find_B1_start --> skip_B1 : locate previous block
    skip_B1 --> copy_B1 : start copying n-2 block
    copy_B1 --> B1_goto_end : write x
    B1_goto_end --> B1_return : append 0
    B1_return --> copy_B1 : return to x
    
    copy_B1 --> copy_B2 : B1 copied
    copy_B2 --> B2_goto_end : write y
    B2_goto_end --> B2_return : append 0
    B2_return --> copy_B2 : return to y
    
    copy_B2 --> restore_B2 : B2 copied
    restore_B2 --> rewind : restore y to 0, start over
    
    find_1 --> cleanup_goto_end : out of 1s!
    cleanup_goto_end --> cleanup_skip_ans : reach end of output
    cleanup_skip_ans --> cleanup_erase : skip rightmost zeroes
    cleanup_erase --> cleanup_finish : erase everything else
    cleanup_finish --> q_accept : leave tape clean
    
    q_accept --> [*]
```
