<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

# Node.js Homework List

## Node.js Homework 1

<details close>
<summary><i>Question1 Content</i></summary> </br>

Hepimizin Matematik derslerinden bildiği üzere Dairenin Alanı = π x r2 şeklinde hesaplanır. Node.JS Javascript çalışma ortamında yarıçap değerini konsoldan parametre olarak girerek alanı bulmaya çalışacağız.
Konsol çıktısı: Yarıçapı (Yarıçap) olan dairenin alanı: (Alan) şeklinde olmalıdır.

```js
const argument = process.argv.slice(2);

function alanBul(r) {
  let alan = Math.PI.toFixed(2) * r ** 2;
  console.log(`Yarıçapı ${r} olan dairenin alanı: ${alan}`);
}

alanBul(argument[0]);
```

</details>

&nbsp;
&nbsp;

---

## Node.js Homework 2

<details close>
<summary> <i>Question2 Content</i> </summary> </br>

Blog oluşturmaya hazır mısınız? Konsol ekranında postlarımızı sıralayalım, sonrasında yeni bir post oluşturalım ve yeni post ile birlikte postlarımızı tekrar sıralayalım.

```js
const posts = [
  { blog: "Blog 1", description: "Lorem Ipsum Dolor 1" },
  { blog: "Blog 2", description: "Lorem Ipsum Dolor 2" },
  { blog: "Blog 3", description: "Lorem Ipsum Dolor 3" },
  { blog: "Blog 4", description: "Lorem Ipsum Dolor 4" },
  { blog: "Blog 5", description: "Lorem Ipsum Dolor 5" },
];

const listPost = () => {
  posts.map((post) => {
    console.log(post);
  });
};

const addPost = (newPost, callback) => {
  posts.push(newPost);
  callback();
};

addPost({ blog: "Blog  6", description: "Lorem Ipsum Dolor 6" }, listPost);
```

</details>

&nbsp;
&nbsp;

---

## Node.js Homework 3

<details close>

  <summary><i>Question3 Content</i></summary> </br>
  
  1. Daire alan : circleArea ve daire çevre : circleCircumference fonksiyonları içeren ve consola sonuçları
  yazdıran circle.js dosyası oluşturunuz.
  2. Module.exports yöntemi ile fonksiyonları oluştururken export ediniz.
  3. require ve object destructing kullanarak index.js dosyasında yarıçap (r) 5 olacak şekilde ekran çıktısını alınız.

```js
// circle.js

const circleArea = (r) => {
  return Math.PI * r ** 2;
};

const circleCircumFerence = (r) => {
  return 2 * Math.PI * r;
};

module.exports = {
  circleArea,
  circleCircumFerence,
};
```

```js
// index.js

const { circleArea, circleCircumFerence } = require("./circle");

console.log(`Dairenin Alanı: ${circleArea(4)} `);
console.log(`Dairenin Çevresi: ${circleCircumFerence(4)} `);
```

</details>

&nbsp;
&nbsp;

---

## Node.js Homework 4

<details close>
  <summary><i>Question4 Content</i></summary> </br>

Node.js <strong><i>FS Modülü</i></strong> kullanarak CRUD işlemleri yapacağız.

1. employees.json dosyası oluşturalım ve içerisine {"name": "Employee 1 Name", "salary": 2000} verisini ekleyelim. (CREATE)
2. Bu veriyi okuyalım. (READ)
3. Bu veriyi güncelleyelim. (UPDATE)
4. Dosyayı silelim. (DELETE)

```js
//? Employee Added

import { writeFile } from "node:fs";
writeFile(
  "employees.json",
  '{"name" : "Employee 1 Name", "salary" : 2000 }',
  "utf8",
  (err) => {
    if (err) throw err;
    console.log("Employee Created");
  }
);

//? Employee Read

import { readFile } from "node:fs";
readFile("employees.json", "utf8", (err, data) => {
  if (err) throw err;
  console.log("Employees Loading...");
  console.log(data);
});

//? Employee Updated (New Employee Added)

import { appendFile } from "node:fs";
appendFile(
  "employees.json",
  '\n{"name" : "Employee 2 Name", "salary" : 2500}',
  (err) => {
    if (err) throw err;
    console.log("New Employee Added");
  }
);

//? Employee File Deleted

import { unlink } from "node:fs";
unlink("employees.json", (err) => {
  if (err) throw err;
  console.log("Employee.json deleted");
});
```

</details>

&nbsp;
&nbsp;

---

## Node.js Homework 5

<details close>
  <summary><i>Question5 Content</i></summary> </br>

Kendi bilgisayarımızda aşağıdaki özellikleri kullanarak sunucumuzu yazalım.

1. createServer metodunu kullanacağız.
2. index, hakkimda ve iletisim sayfaları oluşturalım.
3. Sayfalara içerik olarak xxx sayfasına hoşgeldiniz şeklinde başlıkları yazdıralım.
4. port numarası olarak 5000'i kullanalım.

```js
const http = require("http");

const server = http.createServer((req, res) => {
  const url = req.url;

  if (url === "/") {
    res.writeHead(200, { "Content-Type": "text/html" });
    res.write("<h2>INDEX SAYFASI</h2>");
  } else if (url === "/hakkimda") {
    res.writeHead(200, { "Content-Type": "text/html" });
    res.write("<h2>HAKKIMDA SAYFASI</h2>");
  } else if (url === "/iletisim") {
    res.writeHead(200, { "Content-Type": "text/html" });
    res.write("<h2>ILETISIM SAYFASI</h2>");
  } else {
    res.writeHead(404, { "Content-Type": "text/html" });
    res.write("<h2>404 SAYFA BULUNAMADI</h2>");
  }

  console.log("Bir istek gönderildi.");
  res.end();
});

const port = 5000;
server.listen(port, () => {
  console.log(`Sunucu Port ${port} de Başlatıldı.`);
});
```

</details>

&nbsp;
&nbsp;

---

## Node.js Homework 6

<details close>
  <summary><i>Question6 Content</i></summary> </br>
    
  Öncelikle şunu belirteyim. Koa.js hakkında konuşmadığımızı biliyorum ve bu ödev ilk aşamada bizi zorlayacak. Buradaki amacım yeni bir teknolojiye başlama cesareti oluşturmak ve hata yapma özgürlüğümüz olduğunu göstermek.

1. koa paketini indirelim.
2. index, hakkimda ve iletisim sayfaları oluşturalım.
3. Sayfalara içerik olarak xxx sayfasına hoşgeldiniz şeklinde h1 başlıkları yazdıralım.
4. port numarası olarak 3000'i kullanalım.

5. Yontem

```js
const Koa = require("koa");
const app = new Koa();
const port = 3000;

app.use(async (ctx) => {
  const path = ctx.path;

  switch (path) {
    case "/":
      ctx.type = "text/html";
      ctx.body = "<h1>Anasayfaya Hoşgeldiniz</h1>";
      break;
    case "/about":
      ctx.type = "text/html";
      ctx.body = "<h1>Hakkında Sayfasına Hoşgeldiniz</h1>";
      break;
    case "/contact":
      ctx.type = "text/html";
      ctx.body = "<h1>İletişim Sayfasına Hoşgeldiniz</h1>";
      break;
    default:
      ctx.type = "text/html";
      ctx.body = "<h1>Sayfa Bulunamadı</h1>";
      break;
  }
});

app.listen(port, () => {
  console.log(` İşlem ${port} Port Nolu Sayfada Başladı `);
});
```

</details>
