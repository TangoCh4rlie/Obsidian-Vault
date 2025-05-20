2025-05-16
[[prog]]

---

```C
fseek(fp, 0, SEEK_END);  
const long file_size = ftell(fp);  
fseek(fp, 0, SEEK_SET);
```
pour avoir la taille d'un fichier en nombre d'octet`