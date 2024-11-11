# Game Reality | Game Programming #1
---
## Kebutuhan
1. Sudah menginstall Unity Hub dan Unity Editor.
2. Sudah membuat project kosong.
3. Memiliki text editor (Rekomendasi: Visual Studio Code / Microsoft Visual Studio)

---

## Overview
Pada pertemuan ini, kita akan berkenalan dengan Unity Engine. Serta pengenalan terhadap gameObject, komponen-komponennya, dan memanipulasi gameObject.

Terdapat beberapa Checkpoint dimana anggota akan disuruh untuk mempraktekkan hal yang barusan diajari secara mandiri. Di akhir materi, peserta akan diminta membuat projek berupa game sederhana yaitu *Motorcycle Delivery*.

---

## Checkpoint 1
Buat gameObject² yang barusan kita buat lagi dengan spesifikasi seperti sebelumnya!

1. Tambahkan rigidBody2D dan collider2D ke objek 1
2. Tambahkan collider2D ke objek 2

---
## Checkpoint 2
Buat agar gameObject dapat bergerak melingkar!

Tambahkan script berikut ke objek 1
```bash
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class kotak : MonoBehaviour // Setelah public class, sesuaikan namanya dengan nama script kalian
{
    [SerializeField] float forwardSpeed = 0.05f;
    [SerializeField] float rotateSpeed = 1f;
    // Start is called before the first frame update
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()
    {
        transform.Translate(0, forwardSpeed, 0);
        transform.Rotate(0, 0, rotateSpeed);
    }
}
```



## Checkpoint 2 part 2
Buat agar gameObject dapat bergerak melingkar mengikuti arah jarum jam!
```bash
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class kotak : MonoBehaviour // Setelah public class, sesuaikan namanya dengan nama script kalian
{
    [SerializeField] float forwardSpeed = 0.05f;
    [SerializeField] float rotateSpeed = 1f;
    // Start is called before the first frame update
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()
    {
        transform.Translate(0, forwardSpeed, 0);
        transform.Rotate(0, 0, -rotateSpeed);
    }
}
```

## Checkpoint 3
Dengan memanfaatkan trigger/collision, buat agar gameObject dapat bergerak ke kanan dan ke kiri!
```bash
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class kotak : MonoBehaviour // Setelah public class, sesuaikan namanya dengan nama script kalian
{
    [SerializeField] float moveSpeed = 0.05f;
    // Start is called before the first frame update
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()
    {
        transform.Translate(0, moveSpeed * time.DeltaTime, 0);
    }
    private void OnTriggerEnter2D(Collider2D collision)
    {
        if (collision.tag == "Trigger")
        {
            moveSpeed = moveSpeed * -1;
        }
    }
}
```

## Checkpoint 4
Buat agar gameObject dapat bergerak maju/mundur dengan Input.GetAxis!
```bash
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class driver : MonoBehaviour
{
    [SerializeField] float forwardSpeed = 0.05f;
    [SerializeField] float rotateSpeed = 1f;
    // Start is called before the first frame update
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()
    {
        float moveRotation = Input.GetAxis("Horizontal") * rotateSpeed * Time.deltaTime;
        float moveForward = Input.GetAxis("Vertical") * forwardSpeed * Time.deltaTime;
        transform.Translate(0, moveForward, 0);
        transform.Rotate(0, 0, -moveRotation);
    }
}
```

## Projek *Motorcycle Delivery*
Dengan semua yang telah kita pelajari, sekarang saatnya kita praktek membuat game langsung! Buatlah game sederhana dimana kalian memainkan seorang delivery driver untuk mengantar paket ke orang.

Kriteria Minimal:
1. Dapat bergerak
2. Dapat mengambil paket
3. Dapat mengantar paket
4. Dapat nabrak rintangan
5. Terdapat batasan dunia



### Driver Script
```bash
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class driver : MonoBehaviour
{
    [SerializeField] float forwardSpeed = 0.05f;
    [SerializeField] float rotateSpeed = 1f;
    [SerializeField] bool punyaPaket = false;
    [SerializeField] float point = 0;
    // Start is called before the first frame update
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()
    {
        float moveRotation = Input.GetAxis("Horizontal") * rotateSpeed * Time.deltaTime;
        float moveForward = Input.GetAxis("Vertical") * forwardSpeed * Time.deltaTime;
        transform.Translate(0, moveForward, 0);
        transform.Rotate(0, 0, -moveRotation);
    }

    private void OnCollisionEnter2D(Collision2D collision)
    {
        Debug.Log("AW!");
    }

    private void OnTriggerEnter2D(Collider2D collision)
    {
        if (collision.tag == "Paket" && punyaPaket == false)
        {
            Debug.Log("Paket berhasil diambil");
            Destroy(collision.gameObject);
            punyaPaket = true;
            Debug.Log("Poin anda saat ini: " + point);
        }
        else if (collision.tag == "Paket" && punyaPaket == true)
        {
            Debug.Log("Silahkan antar paket yang kamu bawa terlebih dahulu");
            Debug.Log("Poin anda saat ini: " + point);
        }
        if (collision.tag == "Finish" && punyaPaket == true)
        {
            Debug.Log("Paket berhasil diantar!");
            punyaPaket = false;
            point += 5;
            Debug.Log("Poin anda saat ini: " + point);
        }
        else if(collision.tag == "Finish" && punyaPaket == false)
        {
            Debug.Log("MANA PAKETKU!!");
            Debug.Log("Poin anda saat ini: " + point);
        }
    }
}
```
