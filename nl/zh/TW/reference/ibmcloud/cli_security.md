---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-03"

keywords: cli, security cli, ssh keys cli, ssl cli, ibmcloud sl security, certificate cli, ibmcloud sl, sshkey-add, manage security cli

subcollection: cloud-cli

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:tip: .tip}

# 管理安全 SSH 金鑰和 SSL 憑證
{: #sl-manage-security-keys}

SSH 金鑰允許存取裝置，而不必針對裝置上實作的每個公開金鑰使用來自對應用戶端的密碼。藉由將 SSH 金鑰新增至裝置，被賦與 SSH 金鑰的裝置會存取裝置以取得對應金鑰，而不使用密碼。

網站會啟用 SSL 憑證，作為保護使用者的安全措施。它們一般用於您必須將機密資訊傳輸到網站之時。

請使用下列指令來管理 {{site.data.keyword.cloud}} 標準基礎架構 SSH 金鑰及憑證。
{: shortdesc}

## ibmcloud sl security sshkey-add
{: #sl_security_sshkey_add}

新增 SSH 金鑰。
```
ibmcloud sl security sshkey-add LABEL [OPTIONS]
```

<strong>指令選項</strong>：
<dl>
<dt>-f, --in-file</dt>
<dd>要為此金鑰匯入的 id_rsa.pub 檔案。</dd>
<dt>-k, --key</dt>
<dd>實際 SSH 金鑰。</dd>
<dt>--note</dt>
<dd>將與金鑰相關聯的額外附註。</dd>
</dl>

**範例**：
```
ibmcloud sl security sshkey-add -f ~/.ssh/id_rsa.pub --note mykey
```
{: codeblock}

這個指令會從檔案 ~/.ssh/id_rsa.pub 新增 SSH 金鑰及附註 "mykey"。


## ibmcloud sl security sshkey-edit
{: #sl_security_sshkey_edit}

編輯 SSH 金鑰。
```
ibmcloud sl security sshkey-edit IDENTIFIER [OPTIONS]
```

<strong>指令選項</strong>：
<dl>
<dt>--label</dt>
<dd>金鑰的新標籤。</dd>
<dt>--note</dt>
<dd>金鑰的新附註。</dd>
</dl>

**範例**：
```
ibmcloud sl security sshkey-edit 12345678 --label ibmcloud --note testing
```
{: codeblock}

這個指令會更新 ID 為 `12345678` 的 SSH 金鑰、將標籤設為 `ibmcloud`，並將附註設為 `testing`。

## ibmcloud sl security sshkey-list
{: #sl_security_sshkey_list}

列出您帳戶上的 SSH 金鑰。
```
ibmcloud sl security sshkey-list [OPTIONS]
```

<strong>指令選項</strong>：
<dl>
<dt>--sortby</dt>
<dd>直欄排序方式，選項包含：id、label、fingerprint、notes。</dd>
</dl>

**範例**：
```
ibmcloud sl security sshkey-list --sortby label
```
{: codeblock}

 這個指令會列出現行帳戶上的所有 SSH 金鑰，並依標籤排序。

## ibmcloud sl security sshkey-print
{: #sl_security_sshkey_print}

將 SSH 金鑰印出至螢幕。
```
ibmcloud sl security sshkey-print IDENTIFIER [OPTIONS]
```

<strong>指令選項</strong>：
<dl>
<dt>-f, --out-file</dt>
<dd>公用 SSH 金鑰將會寫入此檔案。</dd>
</dl>

**範例**：
```
ibmcloud sl security sshkey-print 12345678 -f ~/mykey.pub
```
{: codeblock}

這個指令會顯示 ID 為 12345678 的 SSH 金鑰的 ID、標籤及附註，並將公開金鑰寫入檔案：~/mykey.pub。

## ibmcloud sl security sshkey-remove
{: #sl_security_sshkey_remove}

永久移除 SSH 金鑰。
```
ibmcloud sl security sshkey-remove IDENTIFIER [OPTIONS]
```

<strong>指令選項</strong>：
<dl>
<dt>-f, --force</dt>
<dd>強制執行作業，而不進行確認。</dd>
</dl>

**範例**：
```
ibmcloud sl security sshkey-remove 12345678 -f
```
{: codeblock}

這個指令會移除 ID 為 `12345678` 的 SSH 金鑰，而不要求確認。

## ibmcloud sl security cert-add
{: #sl_security_cert_add}

新增及上傳 SSL 憑證詳細資料。
```
ibmcloud sl security cert-add [OPTIONS]
```

<strong>指令選項</strong>：
<dl>
<dt>--crt</dt>
<dd>憑證檔。</dd>
<dt>--csr</dt>
<dd>憑證簽署要求檔。</dd>
<dt>--icc</dt>
<dd>中繼憑證檔。</dd>
<dt>--key</dt>
<dd>私密金鑰檔。</dd>
<dt>--notes</dt>
<dd>其他附註。</dd>
</dl>

**範例**：
```
ibmcloud sl security cert-add --crt ~/ibm.com.cert --key ~/ibm.com.key
```
這個指令會新增網域 ibm.com 的憑證檔 ~/ibm.com.cert 及私密金鑰檔 ~/ibm.com.key。

## ibmcloud sl security cert-edit
{: #sl_security_cert_edit}

編輯 SSL 憑證。
```
ibmcloud sl security cert-edit IDENTIFIER [OPTIONS]
```

<strong>指令選項</strong>：
<dl>
<dt>--crt</dt>
<dd>憑證檔。</dd>
<dt>--csr</dt>
<dd>憑證簽署要求檔。</dd>
<dt>--icc</dt>
<dd>中繼憑證檔。</dd>
<dt>--key</dt>
<dd>私密金鑰檔。</dd>
<dt>--notes</dt>
<dd>其他附註。</dd>
</dl>

**範例**：
```
ibmcloud sl security cert-edit 12345678 --key ~/ibm.com.key
```
這個指令會編輯 ID 為 12345678 的憑證，並以檔案 ~/ibm.com.key 來更新其私密金鑰。

## ibmcloud sl security cert-download
{: #sl_security_cert_download}

下載 SSL 憑證及金鑰檔。
```
ibmcloud sl security cert-download IDENTIFIER
```


**範例**：
```
ibmcloud sl security cert-download 12345678
```
  這個指令會將 4 個檔案下載至 ID 為 12345678 的憑證的現行目錄。這 4 個檔案分別為：憑證檔、憑證簽署要求檔、中繼憑證檔及私密金鑰檔。

## ibmcloud sl security cert-list
{: #sl_security_cert_list}

列出您帳戶上的 SSL 憑證。
```
ibmcloud sl security cert-list [OPTIONS]
```

<strong>指令選項</strong>：
<dl>
<dt>--status</dt>
<dd>顯示具有以下狀態的憑證，預設值為：all，選項包含：all、valid、expired。</dd>
<dt>--sortby</dt>
<dd>直欄排序方式，選項包含：id、common_name、days_until_expire、notes。</dd>
</dl>

**範例**：
```
ibmcloud sl security cert-list --status valid --sortby days_until_expire
```
 這個指令會列出現行帳戶上的所有有效憑證，並依有效天數排序。

## ibmcloud sl security cert-remove
{: #sl_security_cert_remove}

移除 SSL 憑證。
```
ibmcloud sl security cert-remove IDENTIFIER [OPTIONS]
```

<strong>指令選項</strong>：
<dl>
<dt>-f, --force</dt>
<dd>強制執行作業，而不進行確認。</dd>
</dl>

**範例**：
```
ibmcloud sl security cert-remove 12345678
```
 這個指令會移除 ID 為 12345678 的憑證。
