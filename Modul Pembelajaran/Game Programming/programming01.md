# Game Reality | Game Programming #1
---
## transform.Rotate()
```bash
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class kotak : MonoBehaviour
{
    // Start is called before the first frame update
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()
    {
        transform.Rotate(0, 0, 1f);
    }
}
```
Note: transform adalah fungsi untuk mengubah nilai pada komponen Transform. Rotate adalah jenis transform yang akan di berlakukan ke gameObject. Yang didalam kurung adalah sumbu x, y, z. Dalam konteks baris kode transform.Rotate(0, 0, 1f) berarti kita akan melakukan transform "Rotate" terhadap gameObject sebanyak 1f kali terhadap sumbu z.

Note: f dituliskan dibelakang angka karena aturan dari Unity itu sendiri untuk menuliskan f dibelakang angka untuk tipe data float.

---
## transform.Translate()
```bash
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class kotak : MonoBehaviour
{
    // Start is called before the first frame update
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()
    {
        transform.Translate(0.1f, 0, 0);
    }
}
```
Note: Kamu dapat mengubah sumbu x atau y atau keduanya (Dalam konteks game 2D, sumbu z tidak akan terlalu digunakan dalam hal Translasi).

---

## Menggabungkan transform.Rotate() dengan transform.Translate() 
---
```bash
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class kotak : MonoBehaviour
{
    // Start is called before the first frame update
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()
    {
        transform.Translate(0.1,0,0);
        transform.Rotate(0, 0, 1f);
    }
}
```
---
## Variabel
```bash
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class kotak : MonoBehaviour
{
    float moveSpeed = 0.5f;
    float rotateSpeed = 1f;
    // Start is called before the first frame update    
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()       
    {
        transform.Translate(moveSpeed, 0, 0);
        transform.Rotate(0, 0, rotateSpeed);
    }
}
```
Note: Perhatikan semua perubahan yang terjadi dari kode sebelumnya!

---
## SerializeField
```bash
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class kotak : MonoBehaviour
{
    [SerializeField] float moveSpeed = 0.5f;
    [SerializeField] float rotateSpeed = 1f;
    // Start is called before the first frame update    
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()       
    {
        transform.Translate(moveSpeed, 0, 0);
        transform.Rotate(0, 0, rotateSpeed);
    }
}
```
---
## OnCollisonEnter2D()
```bash
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class kotak : MonoBehaviour
{
    // Start is called before the first frame update    
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()       
    {
        
    }

    private void OnCollisionEnter2D(Collision2D collision)
    {
        Debug.Log("AW!");
    }
}
```
---
## OnTriggerEnter2D()
```bash
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class kotak : MonoBehaviour
{
    // Start is called before the first frame update    
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()       
    {

    }

    private void OnCollisionEnter2D(Collision2D collision)
    {
        Debug.Log("AW!");
    }
    private void OnTriggerEnter2D(Collider2D collision)
    {
        Debug.Log("Melewati Trigger");
    }
}
```
---
## Menggunakan Tag untuk OnTriggerEnter2D()
```bash
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class kotak : MonoBehaviour
{
    // Start is called before the first frame update    
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()       
    {
        
    }

    private void OnCollisionEnter2D(Collision2D collision)
    {
        Debug.Log("AW!");
    }
    private void OnTriggerEnter2D(Collider2D collision)
    {
        if (collision.tag == "Merah")
        {
            Debug.Log("Melewati Merah");
        }
        if (collision.tag == "Hijau")
        {
            Debug.Log("Melewati Hijau");
        }
    }
}
```
---
## Memanfaatkan Trigger/Collision untuk membuat objek bergerak ke kanan dan ke kiri
### Menggunakan Collision
```bash
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class kotak : MonoBehaviour
{
    [SerializeField] float moveSpeed = 0.5f;
    // Start is called before the first frame update    
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()       
    {
        transform.Translate(moveSpeed, 0, 0);
    }

    private void OnCollisionEnter2D(Collision2D collision)
    {
        moveSpeed = -moveSpeed;
    }
}
```
### Menggunakan Trigger
```bash
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class kotak : MonoBehaviour
{
    [SerializeField] float moveSpeed = 0.5f;
    // Start is called before the first frame update    
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()       
    {
        transform.Translate(moveSpeed, 0, 0);
    }

    private void OnTriggerEnter2D(Collider2D collision)
    {
        moveSpeed = -moveSpeed;
    }
}
```
---
# Terima Kasih, semoga bermanfaat :] !
