# 🎄 Secret Santa Image Steganography Challenge — Solution Summary

## Objective

Extract and decode a hidden flag embedded inside an image file. The challenge hinted that the flag was:

- Hidden in an image (“The picture contains the flag”)
    
- Encrypted (“possibly encrypted by Santa”)
    
- Required investigation, decoding, and analysis
    

The correct flag format used by the platform was `CTF{}`.

---

## Step 1: Identify the File and Rule Out Easy Wins

- Verified the file was a **valid PNG** by checking its magic bytes.
    
- Checked for:
    
    - Appended data after `IEND`
        
    - PNG text chunks (`tEXt`, `iTXt`, `zTXt`)
        
- None were present, indicating the flag was **not stored as metadata or appended data**.
    

**Conclusion:** The flag was likely hidden using **pixel-based steganography**.

---

## Step 2: Extract Least Significant Bits (LSB)

- Converted the image to raw RGB bytes.
    
- Extracted the **least significant bit (LSB)** from every byte.
    
- Repacked bits into bytes using **MSB-first order**.
    

This revealed a long printable sequence:

`34:XGU{Xs1i5gn@hh_VmxibkG10m_1h_ufm!}Uc`

Inside this string, the meaningful payload was:

`Xs1i5gn@hh_VmxibkG10m_1h_ufm!`

**Conclusion:**  
The LSB extraction was correct. The payload was intentionally encrypted.

---

## Step 3: Identify the Encryption Layers

The challenge hint (“encrypted by Santa”) strongly suggested **classic substitution ciphers**, which are common in holiday-themed CTFs.

### Applied cipher sequence:

1. **ROT13**
    
2. **Atbash**
    
3. **ROT13 again**
    

Applying this exact sequence to the extracted payload produced:

`Ch1r5tm@ss_EncrypT10n_1s_fun!`

This is readable **leetspeak**, not plain English.

---

## Step 4: Submit the Correct Flag (Important Insight)

An initial instinct was to “clean” the text into normal English:

`Christmas_Encryption_is_fun!`

However, the platform **rejected all cleaned versions**.

The correct submission was the **leet-encoded plaintext**, exactly as produced by the cipher chain.

---

## ✅ Final Flag

`CTF{Ch1r5tm@ss_EncrypT10n_1s_fun!}`

---

## Key Takeaways

- Do **not over-normalize** decrypted output — CTFs often expect the _exact cipher result_.
    
- Always trust:
    
    - Bit extraction results
        
    - Cipher outputs
        
    - Platform flag format consistency
        
- “Santa” or holiday hints often imply **ROT13 + Atbash** chains.