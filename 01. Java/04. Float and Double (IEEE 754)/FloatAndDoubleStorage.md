In IEEE 754 representation, **float (32-bit)** and **double (64-bit)** values are stored in memory using a **sign bit, exponent, and mantissa (significand)**. Here's how they are structured:

---

## **1. IEEE 754 Single-Precision (32-bit `float`)**
| **Component** | **Sign (S)** | **Exponent (E)** | **Mantissa (M)** |
|--------------|-------------|------------------|------------------|
| **Bits**     | 1 bit       | 8 bits           | 23 bits          |
| **Position** | Bit 31      | Bits 30–23       | Bits 22–0        |

### **Formula:**
\[
(-1)^S \times (1 + M) \times 2^{(E - 127)}
\]

### **Example: Storing `-13.625` as a `float`**
1. **Convert to binary:**
   - Sign: Negative → \( S = 1 \)
   - Integer part: \( 13 = 1101_2 \)
   - Fractional part: \( 0.625 = 0.101_2 \) (since \( 0.5 + 0.125 = 0.625 \))
   - Full binary: \( 1101.101_2 \)

2. **Normalize (scientific notation):**
   - \( 1.101101 \times 2^3 \)

3. **Extract components:**
   - **Sign (S):** `1` (negative)
   - **Exponent (E):** \( 3 + 127 = 130 \) → `10000010` (8 bits)
   - **Mantissa (M):** `10110100000000000000000` (23 bits, drop leading `1`)

4. **Final 32-bit representation (hex):**
   ```
   1 10000010 10110100000000000000000 → C15A0000
   ```

---

## **2. IEEE 754 Double-Precision (64-bit `double`)**
| **Component** | **Sign (S)** | **Exponent (E)** | **Mantissa (M)** |
|--------------|-------------|------------------|------------------|
| **Bits**     | 1 bit       | 11 bits          | 52 bits          |
| **Position** | Bit 63      | Bits 62–52       | Bits 51–0        |

### **Formula:**
\[
(-1)^S \times (1 + M) \times 2^{(E - 1023)}
\]

### **Example: Storing `-13.625` as a `double`**
1. **Binary representation remains the same:**
   - \( 1101.101_2 = 1.101101 \times 2^3 \)

2. **Extract components:**
   - **Sign (S):** `1` (negative)
   - **Exponent (E):** \( 3 + 1023 = 1026 \) → `10000000010` (11 bits)
   - **Mantissa (M):** `101101000...0` (52 bits, drop leading `1`)

3. **Final 64-bit representation (hex):**
   ```
   1 10000000010 1011010000000000000000000000000000000000000000000000 → C02D400000000000
   ```

---

## **Special Cases**
| **Case**         | **Exponent (E)** | **Mantissa (M)** | **Meaning** |
|------------------|------------------|------------------|-------------|
| **Zero**         | All `0`          | All `0`          | \( \pm 0 \) |
| **Subnormal**    | All `0`          | Non-zero         | \( (-1)^S \times 0.M \times 2^{-126} \) (float) |
| **Infinity**     | All `1`          | All `0`          | \( \pm \infty \) |
| **NaN**          | All `1`          | Non-zero         | Not a Number |

---

### **Summary**
- **Float (32-bit):** `1 sign bit | 8 exponent bits (bias=127) | 23 mantissa bits`
- **Double (64-bit):** `1 sign bit | 11 exponent bits (bias=1023) | 52 mantissa bits`
- **Normalized form:** \( (-1)^S \times (1.M) \times 2^{(E - \text{bias})} \)
- **Subnormal numbers** allow representation of very small numbers near zero.

This format ensures efficient storage while maintaining precision for floating-point arithmetic.