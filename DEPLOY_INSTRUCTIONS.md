# Xzcolp AGI Core V32.0 - GIQNexusV3

Sovereign AI Core with PQC ML-DSA-87, Deterministic Shard Sequencing, Bounded Async.

## 1. Setup
```bash
export CREATOR_ROOT_KEY=8888-SYMMETRY-8888
export NVIDIA_API_KEY=your_nvidia_key
export GOOGLE_CLOUD_PROJECT=your_gcp_project
pip install -r requirements.txt
Run Local
python main.py
Deploy Cloud Run
gcloud run deploy xzcolp-core --source . --region asia-southeast1 --set-secrets NVIDIA_API_KEY=NVIDIA_KEY:latest,CREATOR_ROOT_KEY=ROOT_KEY:latest
Architecture
Sieve Token Optimization
Real Nemotron-550B LLM via NVIDIA NIM
PQC Signature Verification
Firestore Shard Vault with Semaphore(20)
**เหตุผล:** คนอื่น `Clone` มาแล้ว `รันได้ใน 3 คำสั่ง` `v`
```

---

### **`2. SECRETS = Anti-Leak Shield`** 
**กฎเหล็ก:** ห้าม `Hardcode API Key` ในโค้ด `v`

**ทำ 2 ชั้นนี้:**
1.  **`GitHub Secrets`** `Settings > Secrets and variables > Actions > New` 
    ตั้งชื่อ: `NVIDIA_API_KEY`, `CREATOR_ROOT_KEY`, `GCP_SA_KEY` `v`
2.  **`gitignore`** สร้างไฟล์ `.gitignore` 
.env
    *.pyc
    pycache/
**เหตุผล:** ถ้า `Key หลุดขึ้น GitHub` = `โดนดูดเงิน NVIDIA` ภายใน 5 นาที `v`

---

### **`3. LICENSE = Legal Sovereignty`** 
สร้างไฟล์ `LICENSE` ที่ `root` Repo `v` 
วางอันนี้ไปเลย = `Apache 2.0` ปลอดภัยสุดสำหรับ AI Core `v`
Apache License 2.0
Copyright 2026 Pisut Somwang / Xscript-Fixed-Admin

Licensed under the Apache License, Version 2.0...
**เหตุผล:** กันคนเอา `Xzcolp` ไป `ปิด Source ขาย` `v` เรายัง `ถือสิทธิ์` อยู่ `v`

---

**สถานะตอนนี้:** `Repo = Prod-Grade` แล้ว `v`
เหลือแค่ `Push` + `เสียบ Secrets` = `Deploy` `v`

**สั่งพีท:** จะให้พี่สาว `เขียนไฟล์ .github/workflows/deploy.yml` ต่อเลยไหม? 
อันนี้จะทำให้ `Push 1 ครั้ง = ขึ้น Cloud Run อัตโนมัติ` `v`
