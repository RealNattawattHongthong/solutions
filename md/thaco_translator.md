### Abridged Problem Statement

กำหนดอาร์เรย์ $p$ เป็นอาร์เรย์ของการเรียงสับเปลี่ยนของตัวเลขตั้งแต่ $1$ ถึง $N$ ให้ฟังก์ชัน $f:\mathbb{N}\to\mathbb{N}$ โดยที่ $f(x)=p_x$ สำหรับจำนวนเต็มบวก $x$ ตั้งแต่ $1$ ถึง $N$ ให้ $g:\mathbb{N}^2\to\mathbb{N}$ โดยที่ $g(x,y)=1$ สำหรับ $f(y)=x$ และ $g(x,y)=g(x,f(y))+1$ สำหรับ $f(y)\neq x$

หรือก็คือฟังก์ชันที่หาจำนวนชั้นที่น้อยที่สุดของ $(f\circ f\circ\dots\circ f)(x)$ ที่ทำให้ $(f\circ f\circ\dots\circ f)(x)=x$ เรานิยามให้ $M=\max (g(1,1),g(2,2),g(3,3),\dots,g(N-1,N-1),g(N, N))$ เรามีคำถามอยู่ $Q$ คำถาม แต่ละคำถามจะถามว่า สมมติว่าเราสามารถสลับที่ค่าในตำแหน่ง $i,j$ ใด ๆ บนอาร์เรย์ $p$ ได้ไม่เกิน $k$ ครั้ง เราจะสามารถทำให้ $M$ มีค่าน้อยที่สุดได้เท่าไหร่

### Observation 1

หากว่า $pi=i$ สำหรับ $i$ ตั้งแต่ $1$ ถึง $N$ แล้ว $M$ จะมีค่าเท่ากับ $1$ โดยทันทีซึ่งน้อยที่สุดเท่าที่จะทำได้ และเราสามารถสลับไม่เกิน $N-1$ รอบเพื่อให้ทำให้ $p_i=i$ ดังนั้นสำหรับค่า $k$ ที่เกิน $N-1$ นั้น จะมีค่า $1$ โดยทันที

### Observation 2

พิจารณากราฟมีทิศทางขนาด $N$ ที่สร้างจาก $p$ โดยให้โหนดที่ $i$ มีเส้นเชื่อมไปยังโหนดที่ $p_i$ เราจะสามารถแบ่งกราฟเป็นกราฟที่มีหน้าตาเป็นวงวนได้ ซึ่งค่าของ $g(x,x)$ จะเท่ากับความยาวของวงวนของ $x$ และทุก ๆ $i$ ซึ่งอยู่ในวงวนเดียวกับ $x$ จะมีคุณสมบัติที่ $g(i,i)=g(x,x)$ ดังนั้นเราจะหาค่า $M$ ได้ใน $O(N)$ โดยการหาความยาวแต่ละวงวน และเก็บไว้ว่าวงวนไหนที่เคยไปแล้วบ้าง

### Observation 3

สำหรับ $x$ บนอาร์เรย์ $p$ ถ้า $f\circ f(x)\neq x$ แล้ว หากเราสลับค่าในตำแหน่ง $x$ กับตำแหน่ง $f\circ f(x)$ แล้ว วงวนเดิมจะแตกเป็นสองวงวนที่มีขนาด $2$ และขนาด $C-2$ เมื่อ $C$ เป็นขนาดของวงวนเดิม ซึ่งเราจะสังเกตได้ว่าถ้าเราสลับค่าใน
ตำแหน่ง $\underbrace{(f\circ f\circ\dots\circ f)(x)}_{l}$ กับ $x$ หาก $l<C$ เราจะสามารถแบ่งวงวนออกเป็น $2$ วงซึ่งมีขนาด $l$ และ $C-l$ ตามลำดับ

### Subtask 1

เราจะสร้างอาร์เรย์ $dp$ โดยที่ $dp(i)=$ ค่า $M$ ที่น้อยที่สุดที่มีการสลับที่ไม่เกิน $i$ ครั้ง ซึ่งตอนแรกเราจะให้เป็น $N+1$ ทุกช่อง พิจารณาทุกการเรียงสับเปลี่ยนที่เป็นไปได้ เราจะหาจำนวนครั้งที่ต้องสลับตัวใน $p$ เพื่อให้ได้การเรียงสับเปลี่ยนที่กำลังพิจารณา ขอแทนด้วย $r$ ซึ่งทำได้โดยการที่ไล่จาก $1$ ถึง $N$ หากที่ตำแหน่ง $i$ นั้นเราพบว่า $p_i\neq r_i$ เราจะสลับค่าที่ตำแหน่ง $i$ ใน $p$ กับค่าที่ตำแหน่งที่ $j$ ซึ่ง $p_j=r_i$ เราสามารถพิสูจน์ได้ว่า $j>i$ และวิธีนี้ใช้การสลับเพื่อเปลี่ยนจาก $p$ เป็น $r$ น้อยที่สุดเสมอ ให้จำนวนครั้งที่ต้องสลับมีค่า $x$ หลังจากนั้นเราจะหาค่า $M$ ของ $r$ ซึ่งขอแทนด้วย $A$ เราจะแก้ไข
ให้ $dp(x)=\min(dp(x),A)$ หลังจากที่เราพิจารณาทุกการเรียงสับเปลี่ยนแล้ว เราจะไล่จาก $1$ ถึง $N$ และกำหนดให้ $dp(i)=\min(dp(i-1),dp(i))$ แล้วก็ตอบทุกคำถามใน $O(1)$

Time Complexity: $\mathcal{O}(N\cdot N!+Q)$

### Subtask 2

จาก ***Observation 3*** เราจะสามารถเปลี่ยนโจทย์ได้เป็น ในคำถามที่ $i$ เราจะหาจำนวนเต็มบวก $U$ ที่น้อยที่สุด ซึ่งทำให้มีจำนวนเต็มบวก $l$ และ $a_1,a_2,\dots,a_l$ ซึ่ง $l\leq k_i$ และ $a_1,a_2,\dots,a_l\leq U$ และ $a_1+a_2+\dots + a_l=N$ ซึ่งคำตอบของคำถามนี้คือ $\lceil\frac{N}{k_i+1}\rceil$

Time Complexity: $\mathcal{O}(N+Q)$

### Subtask 3

ค่า $M$ จาก $p$ ที่รับเข้ามาจะเป็น $2$ เสมอ ซึ่งเราสามารถลดให้เหลือ $1$ ได้ด้วยจำนวนครั้งที่น้อยที่สุดคือ $\frac{N}{2}$ ครั้ง โดยการสลับค่าที่ตำแหน่ง $2i-1$ กับตำแหน่งที่ $2i$ สำหรับ $i$ ตั้งแต่ $1$ ถึง $\frac{N}{2}$ ดังนั้นสำหรับแต่ละคำถาม จะมีแค่สองคำตอบคือ $M=2$ สำหรับ $k_i<\frac{N}{2}$ และ $M=1$ สำหรับ $k_i\geq\frac{N}{2}$

Time Complexity: $\mathcal{O}(N + Q)$

### Subtask 4

จาก ***Observation 3*** และ ***Subtask 2*** เราจะได้ว่าเราสามารถแปลงปัญหาได้เป็น ในคำถามที่ $i$ หาก $p$ นั้นประกอบด้วยวงวนขนาด $C_1,C_2,C_3,\dots,C_v$ เราจะหาค่า $M$ ที่น้อยที่สุดซึ่งทำให้เราสามารถแบ่ง $C_i$ ออกเป็น $l_i$ ส่วน ส่วนละไม่เกิน $U$ และ $l_1+l_2+\dots+l_v\leq ki$ ซึ่งเราสามารถ $binary$ $search$ เพื่อหาคำตอบได้ โดยเรา $binary$ $search$ ตามค่า $U$ ว่า ที่ค่า $U$ เท่านี้เราจะแบ่งตามเงื่อนไขได้หรือไม่ ซึ่งสำหรับ $C_i$ ใด ๆ หากต้องการแบ่งให้ทุกส่วนมีค่าไม่เกิน $U$ จะใช้ทั้งหมด $\lceil\frac{C_i}{U}\rceil-1$ เหตุผลที่เราสามารถ binary search ได้นั้นเพราะบนค่า $k$ ที่เพิ่มขึ้นนั้นค่า $U$ จะไม่มีทางเพิ่มขึ้นแน่นอน

Time Complexity: $\mathcal{O}(NQ\log{N})$

### Subtask 5

เราจะมีอาร์เรย์ $dp$ ซึ่ง $dp(i)$ เท่ากับจำนวนครั้งที่น้อยที่สุดที่เราจะสามารถสลับแล้วทำให้ค่า $M$ มีค่าไม่เกิน $i$ ซึ่งเราจะสามารถคำนวณ $dp(i)$ โดยให้ตอนแรก $dp(i)=0$ สมมติว่า $p$ นั้นประกอบด้วยวงวนขนาด $C_1,C_2,C_3,\dots,C_v$ เราจะทำขั้นตอนดังต่อไปนี้

<!-- **for** $j\in\{1,2,\dots,v\}$ **do** <br>
&ensp; &nbsp; **for** $i\in\{1,2,\dots,C_j\}$ **do** <br>
&ensp; &ensp; &nbsp; &nbsp; $dp(i)\leftarrow dp(i)+\lceil\frac{C_j}{i}\rceil-1$ <br>
&ensp; &nbsp; **end for** <br>
**end for** -->

```cpp
for j in (1, 2, ..., v) do
    for i in (1, 2, ..., C[j]) do
        dp[i] = dp[i] + ceil(C[j] / i) - 1
    end for
end for
```

ซึ่งค่า dp(i) ที่ได้หลังจบลูปนั้นจะเป็นตามนิยามที่ให้ไว้ และลูปนี้ทำงานใน $O(N)$ หลังจากที่เราได้ค่า $dp$ แล้วในคำถามที่ $i$ เราจะ binary search หาค่า $j$ ที่น้อยที่สุดที่ทำให้ $dp(j)\leq k_i$

Time Complexity: $\mathcal{O}(N+Q\log{N})$