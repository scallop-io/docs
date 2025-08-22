# 怎麼在Scallop上借款

## 借款

在 Scallop 平台上借款時，您需要先存入抵押品，以便借到所需的資產。然而，在進行存款和借款之前，您需要先創建一個[債務](../scallop-lend/zhai-wu.md)。

<figure><img src="../.gitbook/assets/image (7).png" alt="" width="563"><figcaption><p>創建債務帳戶</p></figcaption></figure>

### 存入抵押品

您可以選擇各類資產做為抵押品

<figure><img src="../.gitbook/assets/image (10).png" alt="" width="563"><figcaption><p>抵押品池</p></figcaption></figure>

輸入您想要存入的資產數量

<figure><img src="../.gitbook/assets/image (9).png" alt="" width="375"><figcaption><p>存入 SUI 做為抵押品</p></figcaption></figure>

> 您不會因為存入抵押品獲得任何收益

<figure><img src="../.gitbook/assets/image (11).png" alt="" width="563"><figcaption><p>抵押品資產池</p></figcaption></figure>

如上圖所示，您可以查看您在抵押池中存入資產的摘要儀表板。該摘要儀表板包含四個部分：

1. **可用抵押品**: 可借款資產的總美元價值。
2. **已存入抵押品**: 已存入抵押池的資產總美元價值。
3. **風險水平**: 表示債務帳戶的安全狀態，計算方式為「借款價值加權」除以「所需抵押品價值」。讀數為100%時表示達到清算門檻，即使超過這個數值也是如此。
4. **抵押品組合**: 列出您提供給抵押池的資產。

### 借款

在將資產存入抵押池後，您可以從借貸池中選擇您想借的資產。輸入您想從借貸池中借出的金額，並考慮到借款金額越高，您的債務風險水平就越高，這可能導致您的債務本被清算。

<figure><img src="../.gitbook/assets/image (12).png" alt="" width="563"><figcaption><p>借出資產</p></figcaption></figure>

如上圖所示，存在借款費用參數，這意味著每次您借款時，都將被收取0.3%的費用。

<figure><img src="../.gitbook/assets/image (13).png" alt="" width="563"><figcaption><p>借款儀錶板</p></figcaption></figure>

* **可用抵押品**: 可以借款的總美元資產。
* **已借款總負債**: 已借出的總美元資產。
* **風險水平**: 表示債務帳戶的安全狀態，根據「借款價值加權」除以「所需抵押品價值」計算。當讀數達到100%時，表示已達到清算門檻；即使超過這個數值，它仍然會保持在100%。
* **債務組合**: 您已借出的資產列表。

#### 借款 APR & 獎勵 APR

您可能會注意到，在借貸池中有借款年利率（Borrow APR）和獎勵年利率（Reward APR）兩個欄位。

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption><p>借款池</p></figcaption></figure>

借款年利率（Borrow APR）是指貸款利率，而獎勵年利率（Reward APR）則是提供給借款用戶的激勵計劃利率。當獎勵年利率高於借款年利率時，這意味著通過借款，您可以獲得正收益。

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption><p>取得激勵獎勵</p></figcaption></figure>

您也可以在該面板中領取借款獎勵。因此，如果您抵押 sCoin 並同時借入具有獎勵年利率的資產，這意味著您將同時從借貸池和借款池獲得獎勵激勵計劃的回報。

### 避免清算

為避免被清算，您可以將債務的風險水平設置為低於100%。如果您的債務本風險水平超過100%，Scallop將啟動[軟清算](../scallop-lend/liquidations.md#ruan-qing-suan)機制。

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption><p>借款儀錶板</p></figcaption></figure>

在這個例子中，債務本的風險水平已達到93%，如果超過100%，我們的抵押資產將被清算。為了防止這種情況發生，我們可以償還之前借入的資產。由於借入的資產僅有USDC，我們可以償還這種資產以降低風險水平百分比。

<figure><img src="../.gitbook/assets/image (17).png" alt="" width="375"><figcaption><p>還款</p></figcaption></figure>

在還款之後，風險水平會隨之下降。

<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption><p>借款儀錶板</p></figcaption></figure>

#### 提領抵押品

在提取抵押品之前，請確保已償還所有借入的資產及其利息。一旦您償還了所有債務資產，就可以從抵押池中提取所有資產。

<figure><img src="../.gitbook/assets/image (21).png" alt="" width="375"><figcaption><p>提領抵押品</p></figcaption></figure>

訪問[借款](../scallop-lend/borrowing.md)[清算](../scallop-lend/liquidations.md)以獲得更多資訊
