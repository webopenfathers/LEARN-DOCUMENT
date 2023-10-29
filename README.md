# 慕慕货运
- https://coding.imooc.com/learn/list/644.html

<script setup>
import { ref } from "vue";
import JsPDF from "jspdf";
import html2canvas from "html2canvas";

const sectionRef = ref(null)

const downloadPDF = async () => {
  const pdf = new JsPDF(undefined, 'pt', 'a4');
  const item = sectionRef.value.querySelectorAll('.p')

  const pdfHeight = 841
  let position = 30;

  for (let i = 0; i < item.length; i++) {
    const canvas = await html2canvas(item[i], {
      background: '#FFF',
      scale: 2
    })
    const imgWidth = canvas.width, imgHeight = canvas.height
    const pdfImg = canvas.toDataURL('image/jpeg', 1.0)
    // a4纸的尺寸 [595.28,841.89]
    const contentWidth = 535; // 图片宽度 左右留白30 减去60
    // 535/? = imgWidth/imgHeight
    const contentHeight = 535 * imgHeight / imgWidth

    if (position + contentHeight > pdfHeight) {
      pdf.addPage()
      position = 30
      const img = sectionRef.value.querySelector('img')
      pdf.addImage(img, 'JPEG', 30, 10, 100, 40)
      position += 40
    }
    pdf.addImage(pdfImg, 'JPEG', 30, position, contentWidth, contentHeight)
    position += contentHeight
  }


  pdf.save('合同.pdf')
}
</script>

<template>
  <button @click="downloadPDF" style="padding: 10px">下载pdf</button>
  <div class="section" ref="sectionRef">
    <div class="p">
      <img src="./assets/l.png" alt="">
      <h1>房屋租赁短租合同范本</h1>
      <p>
        <span><span>出租方：</span>________(以下简称甲方)&nbsp;&nbsp;&nbsp;身份证：&nbsp;________________</span><span></span>
      </p>
      <p>
        <span><span>承租方：</span>________(以下简称乙方)&nbsp;&nbsp;&nbsp;身份证：&nbsp;________________</span><span
      ></span>
      </p>
      <p>
        <span><span>根据甲、乙双方在自愿、平等、互利的基础上，经协商一致，为明确双方之间的权利义务关系，就甲方将其合法拥有的房屋出租给乙方使用，乙方承租甲方房屋事宜，订立本合同。</span></span><span></span>
      </p>
    </div>
    <p class="p"><span><span>一、房屋地址：</span>&nbsp;________________________________________________</span><span></span></p>
    <p class="p"><span><span>二、租赁期限及约定</span></span><span></span></p>
    <p class="p"><span>1、该房屋租赁期自______年_____月_____日起至_____年_____月_____日止。</span><span></span></p>
    <p class="p"><span>2、房屋租金：每月_____元。1次性交________个月房租，另付________个月房租作为押金。总计________&nbsp;元。(大写：___万___仟___佰____拾____元整)。房屋终止租赁，甲方验收无误后，将押金退还乙方，不计利息。</span><span></span></p>
    <p class="p"><span>3、乙方向甲方承诺，租赁该房屋仅作为普通住房使用。</span><span></span></p>
    <p class="p"><span>4、租赁期间任何一方基于正当合理理由提出终止合同，须提前1个月告知对方，甲方不得拒绝退还乙方押金。</span><span></span></p>
    <p class="p"><span>5、租赁期满，甲方有权收回出租房屋，乙方应如期交还。乙方如要求续租，则必须在租赁期满前一个月内通知甲方，经甲方同意后，重新签订租赁合同。</span><span></span></p>
    <p class="p"><span><span>三、房屋修缮与使用</span></span><span></span></p>
    <p class="p"><span>1、在租赁期内，甲方应保证出租房屋的使用安全。</span><span></span></p>
    <p class="p"><span>2、乙方应合理使用其所承租的房屋及其附属设施。如乙方因使用不当造成房屋及设施损坏的，尤其是冰箱、洗衣机、热水器、空调等重要家电，乙方自费负责维修。</span><span></span></p>
    <p class="p"><span>3、房屋租赁期间，乙方使用的水电费自行缴付。</span><span></span></p>
    <p class="p"><span><span>四、争议解决办法</span></span><span></span></p>
    <p class="p"><span><font>若甲乙双方因意见不一造成纠纷，先协商解决，协商不成由商不成由当地人民法院仲裁解决。</font></span><span></span></p>
    <p class="p"><span><span>六、本协议一式两份，甲</span>.乙各执一份，签字后即行生效。</span><span></span></p>
    <p class="p"><span><span>七、补充条款</span></span><span></span></p>
    <p class="p"><span>_____________________________________________________________________________</span><span></span></p>
    <p class="p">
      <span><span>甲方签字：</span>________</span><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span
    ><span>乙方签字：</span>________</span><span></span>
    </p>
    <p class="p"><span><span>联系方式：</span>________</span><span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span>&nbsp;<span>联系方式：</span>________</span><span></span></p>
  </div>
</template>

<style scoped>
h1 {
  font-size: 24pt;
  text-align: center;
  margin-bottom: 40pt;
}

.section {
  margin: 72pt auto;
  line-height: 2;
  width: 595px;
  position: relative;
}

.section img {
  width: 100px;
  height: auto;
  position: absolute;
  top: 0;
  left: 0;
}
</style>
