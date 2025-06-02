2025-05-16
[[prog]]

---

```C
fseek(fp, 0, SEEK_END);  
const long file_size = ftell(fp);  
fseek(fp, 0, SEEK_SET);
```
pour avoir la taille d'un fichier en nombre d'octet

## LSB MSB

```C
char test = 0x14;  
  
// least significant bit  
printf("%x", test >> 4);  
// most significant bit  
printf("%x", test & 0x0F);
```