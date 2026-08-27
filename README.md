# migoapi

Migoo auto-task API — image generation via GitHub.

## Struktur

```
migoapi/
├── image.txt              ← instruksi generate gambar
├── responses/             ← hasil response auto-task
│   └── response_image_{idtask}.txt
└── README.md
```

## Format Instruksi (`image.txt`)

```
[idtask:2831, GPT-Image-2, 1K, 9x16, count 1], prompt : buatkan kepala bebek badan singa
```

Field:
- `idtask` — ID unik task
- Model — model yang digunakan (GPT-Image-2)
- Resolusi — 1K / 2K / 4K
- Rasio — 9x16, 16x9, 1x1
- `count` — jumlah gambar
- `prompt` — deskripsi gambar

## Format Response (`responses/response_image_{idtask}.txt`)

**Sukses:**
```
idtask: 2831
status: done
prompt: buatkan kepala bebek badan singa
images:
- https://public-url/image1.png
```

**Gagal:**
```
idtask: 2831
status: error
ERROR: generation failed — timeout
```

## Aturan

- Setelah response ditulis, `[DONE]` di-append di akhir `image.txt`
- Jika `image.txt` sudah ada `[DONE]`, auto-task tidak akan eksekusi
- Interval auto-task: 1 menit
