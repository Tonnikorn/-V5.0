<!DOCTYPE html>
<html lang="th">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>โปรแกรมคำนวณราคาเห็ดแดง</title>
<style>
    body {
        font-family: 'Arial', sans-serif;
        background-color: #FFF8F0;
        margin: 0;
        padding: 0;
        display: flex;
        justify-content: center;
        align-items: center;
        min-height: 100vh;
    }
    .container {
        width: 420px;
        background-color: #FFFDF5;
        padding: 30px 25px;
        border-radius: 25px;
        box-shadow: 0 8px 25px rgba(0,0,0,0.25);
        display: flex;
        flex-direction: column;
        align-items: center;
    }
    h1 { 
        text-align: center; 
        color: #C1272D; 
        margin-bottom: 35px; 
        font-size: 36px; 
    }
    .input-group {
        width: 100%;
        display: flex;
        flex-direction: column;
        align-items: center;
        margin-bottom: 20px;
        padding: 15px;
        border-radius: 15px;
        border: 3px solid #CCC;
        box-shadow: inset 0 0 10px rgba(0,0,0,0.05);
    }
    label { 
        font-size: 24px; 
        font-weight: bold;
        margin-bottom: 10px;
        text-align: center;
    }
    input[type="text"] {
        width: 90%; 
        padding: 14px; 
        font-size: 24px;
        border-radius: 12px; 
        border: 2px solid #AAA; 
        outline: none;
        text-align: center;
    }
    input[type="text"]:focus {
        border-color: #C1272D;
        box-shadow: 0 0 10px rgba(193, 39, 45, 0.3);
    }
    button {
        width: 90%; 
        padding: 18px; 
        font-size: 26px;
        background-color: #C1272D; 
        color: white; 
        border: none;
        border-radius: 20px; 
        cursor: pointer; 
        margin-top: 25px;
        font-weight: bold;
        box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        transition: 0.2s;
    }
    button:hover { 
        background-color: #FF4C4C; 
        transform: translateY(-2px);
    }
    .result { 
        width: 100%;
        margin-top: 30px; 
        font-size: 28px; 
        font-weight: bold; 
        text-align: center; 
        color: #1C6E8C; 
        line-height: 2;
        background-color: #F0F8FF;
        padding: 20px;
        border-radius: 15px;
        border: 2px solid #1C6E8C;
        box-shadow: inset 0 0 8px rgba(28,110,140,0.2);
    }
    #group-large { background-color: #FFE5E5; border-color: #FF9999; }
    #group-small { background-color: #E5FFE5; border-color: #99FF99; }
    #group-bloom { background-color: #E5E5FF; border-color: #9999FF; }

    @media (max-width: 500px) {
        .container { width: 90%; padding: 20px; }
        h1 { font-size: 32px; margin-bottom: 25px; }
        label { font-size: 22px; }
        input[type="text"] { font-size: 22px; }
        button { font-size: 24px; }
        .result { font-size: 24px; }
    }
</style>
</head>
<body>
<div class="container">
    <h1>โปรแกรมซื้อขายเห็ดแดง</h1>

    <div class="input-group" id="group-large">
        <label for="largeWeight">จี๋ใหญ่ (กิโลกรัม)</label>
        <input type="text" id="largeWeight" placeholder="กรอกน้ำหนัก">
    </div>

    <div class="input-group" id="group-small">
        <label for="smallWeight">จี๋เล็ก (กิโลกรัม)</label>
        <input type="text" id="smallWeight" placeholder="กรอกน้ำหนัก">
    </div>

    <div class="input-group" id="group-bloom">
        <label for="bloomWeight">เห็ดบาน (กิโลกรัม)</label>
        <input type="text" id="bloomWeight" placeholder="กรอกน้ำหนัก">
    </div>

    <button type="button" id="calculateBtn">คำนวณราคา</button>

    <div class="result" id="total"></div>
</div>

<script>
function calculateWeight(inputId) {
    const input = document.getElementById(inputId).value || '0';
    try {
        const value = Function('"use strict"; return (' + input + ')')();
        return Math.max(parseFloat(value) || 0, 0);
    } catch {
        return 0;
    }
}

document.getElementById('calculateBtn').addEventListener('click', function() {
    const priceLarge = 290;
    const priceSmall = 100;
    const priceBloom = 70;

    const large = calculateWeight('largeWeight');
    const small = calculateWeight('smallWeight');
    const bloom = calculateWeight('bloomWeight');

    const totalLarge = large * priceLarge;
    const totalSmall = small * priceSmall;
    const totalBloom = bloom * priceBloom;
    const total = totalLarge + totalSmall + totalBloom;

    document.getElementById('total').innerHTML = `
        จี๋ใหญ่: ${totalLarge.toLocaleString()} บาท<br>
        จี๋เล็ก: ${totalSmall.toLocaleString()} บาท<br>
        เห็ดบาน: ${totalBloom.toLocaleString()} บาท<br>
        <strong>จำนวนเงินทั้งหมด: ${total.toLocaleString()} บาท</strong>
    `;

    // ล้างค่า
    document.getElementById('largeWeight').value = '';
    document.getElementById('smallWeight').value = '';
    document.getElementById('bloomWeight').value = '';
});
</script>
</body>
</html>
