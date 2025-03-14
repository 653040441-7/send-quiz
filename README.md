# XO website 
 XO Website สามารถกำหนดขนาดของตารางXO  เป็นขนาดใด ๆ ก็ได้ที่มากกว่า 3x3 มีการเก็บประวัติการเล่น เขียนโดยใช้ Vue 3 + TypeScript + Vite ชื่อไฟล์ว่า Test.vue
 > path ของ file ที่เขียน  send-quiz/src/Test.vue
## วิธีการ set up

การ download 

    git clone https://github.com/653040441-7/send-quiz.git
การ set up vite

    npm install -g vite

การ set up vue

    npm install vue @vue/compiler-sfc
    npm install -D @types/vue
การ set up tailwind
 
    npm install -D tailwindcss@latest postcss@latest autoprefixer@latest
## วิธีการ run program
ไปที่โฟลเดอร์ชื่อ send-quiz หรือเปิดโฟลเดอร์ผ่านโปรแกรม vs code 
 

      cd send-quiz
    
  ใน terminal รันคำสั่ง
 

       npm run dev

> หากไม่สามารถ run ได้ใน terminal ของ vs code แนะนำให้รันที่ command prompt โดยตรง

จากนั้นกดลิ้งเพื่อไปยังหน้าเว็ปไซต์

  ##  วิธีการออกแบบโปรแกรม
link figma : [draft tic-tac-toe](https://www.figma.com/design/0ggtmr9kXpAcqZgf8oRxmA/draft-tic-tac-toe?node-id=0-1&t=R1wp8nxPWu4w8BTD-1)

 ใช้สีโทนขาว ดำ ที่มีความแตกต่างกันเหมือนกับ X และ O พยายามจัดองค์ประกอบให้มีความสมมาตร และอยู่ตรงกลาง 
	   
## algorithm





การเก็บข้อมูลจะมีการรับค่าขนาดของตาราง และการเก็บค่า index ของช่องที่แต่ล่ะฝ่ายได้ทำการกด มาคำนวณแถวและคอลัมน์ของช่องที่แต่ล่ะฝ่ายเลือก เก็บแยกกันในตัวแปรประเภท list เพื่อคำนวณวิธีการชนะ
กรณีที่การชนะ

 - รูปแบบของแนวตั้ง หรือแนวนอน

ใช้การนับค่าในลิสต์แถวและคอลัมน์ของแต่ล่ะฝ่าย หากมีค่าที่มีจำนวนเท่ากับขนาดของตาราง ฝ่ายนั้นจะเป็นผู้ชนะ

 - รูปแบบแนวเฉียงบนลงล่าง

ใช้การเทียบว่าเมื่อค่าคอลัมน์และแถวของช่องที่กดมีค่าเดียวกัน จำนวนเท่ากับขนาดของตาราง ฝ่ายนั้นจะเป็นผู้ชนะ

 - รูปแบบแนวล่างขึ้นบน

ใช้การเทียบว่า เมื่อมีกรณีที่นำค่าคอลัมน์และค่าแถวของช่องที่กด มาบวกกันแล้วมีค่าเท่ากับ ขนาดของตาราง + 1 เมื่อค่าคอลัมน์และค่าแถวเริ่มต้นที่ 1
	   
