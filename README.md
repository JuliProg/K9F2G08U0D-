# K9F1G08U0D
Implementation of the K9F1G08U0D chip for the JuliProg programmer

Dependency injection, DI based on MEF framework is used to connect the chip to the programmer.


# Chip parameters

```c#
  ChipAssembly()
        {
            myChip.devManuf = "SAMSUNG";
            myChip.name = "K9F1G08U0D";

            myChip.width = Organization.x8;    // chip width - 8 bit
            myChip.bytesPP = 2048;             // page size - 2048 byte (2Kb)
            myChip.spareBytesPP = 64;          // size Spare Area - 64 byte
            myChip.pagesPB = 64;               // the number of pages per block - 64 
            myChip.bloksPLUN = 1024;           // number of blocks in CE - 1024
            myChip.LUNs = 1;                   // the amount of CE in the chip
            myChip.colAdrCycles = 2;           // cycles for column addressing
            myChip.rowAdrCycles = 2;           // cycles for row addressing 
            myChip.vcc = Vcc.v3_3;             // supply voltage

  ```   

# Chip operations

```c#
//------- Add chip operations ----------------------------------------------------

            myChip.Operations("Reset_FFh").
                   Operations("Erase_60h_D0h").
                   Operations("Read_00h_30h").
                   Operations("PageProgram_80h_10h");
```

# Chip registers (optional)

```c#
//------- Add chip registers ----------------------------------------------------

            myChip.registers.Add(
                "Status Register").
                Size(1).
                Operations("ReadStatus_70h").
                Interpretation("StatusInterpreting@v1");   //From ChipPart\[some].dll



            myChip.registers.Add(
                "Id Register").
                Size(5).
                Operations("ReadId_90h").               
                Interpretation(ID_interpreting);          // From here
                                            
```

# Interpretation of ID-register values ​​(optional)

```c#
          public string ID_interpreting(Register register)
          private string ID_decoding(byte bt, int pos)
```
