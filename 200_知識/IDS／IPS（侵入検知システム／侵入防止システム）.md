IDS/IPSは、ネットワークやシステムへの**不正な侵入や攻撃を検知し、必要に応じて防御する**ためのセキュリティシステムです。両者は密接に関連しており、しばしばセットで語られますが、その役割には重要な違いがあります。

### 1. IDS (Intrusion Detection System：侵入検知システム)

IDSは、その名の通り、**「検知」と「通知」**を主な役割とするシステムです。

- **機能**: ネットワークトラフィックやホストのシステムログなどを監視し、不審な活動や攻撃の兆候を検出します。
    
- **動作**: 不審な活動を検知すると、管理者にアラートを送信したり、ログに記録したりするだけで、**自ら通信を遮断するなどの防御アクションは行いません**。
    
- **設置方法**: 通常、ネットワークの通信経路に影響を与えないように、通信のコピー（ミラーポートなど）を監視する形で設置されます。これにより、IDS自体の障害がネットワーク全体に影響を与えるリスクを低減できます。
    

### 2. IPS (Intrusion Prevention System：侵入防止システム)

IPSは、IDSの「検知」機能に加え、**「防御」**を主な役割とするシステムです。

- **機能**: IDSと同様に不審な活動や攻撃の兆候を検出します。
    
- **動作**: 不審な活動を検知すると、**自動的にその通信を遮断したり、攻撃元のIPアドレスをブロックしたりするなど、積極的な防御アクションを実行します**。
    
- **設置方法**: ネットワークの通信経路に**インライン（直列）**で配置されます。これにより、すべてのトラフィックがIPSを通過するため、リアルタイムでの検査と防御が可能になります。
    

### IDSとIPSの主な違い

|特徴|IDS（侵入検知システム）|IPS（侵入防止システム）|
|---|---|---|
|**主な役割**|不正アクセスの「検知」と「通知」|不正アクセスの「検知」と「自動防御（遮断など）」|
|**設置方法**|ネットワークのコピーを監視（インラインではない）|ネットワークの通信経路にインラインで設置|
|**通信への影響**|なし（検知のみ）|障害や誤検知の場合、通信が遮断されるリスクがある|
|**アクション**|管理者への通知、ログ記録|通信遮断、パケット廃棄、攻撃元IPアドレスブロックなど|
|**メリット**|誤検知があっても通信が止まらないため、業務への影響が少ない|脅威を自動的に排除できるため、迅速な対応が可能|
|**デメリット**|手動での対処が必要で、迅速な防御が難しい|誤検知により正常な通信が遮断され、業務に支障が出る可能性|

### 検知方式の種類

IDS/IPSの主な検知方式には以下の2種類があります。

1. **シグネチャ型（Signature-based detection）**:
    
    - **仕組み**: 既知の攻撃パターン（シグネチャ）のデータベースと、通過する通信の内容を照合し、一致した場合に脅威と判断します。ウイルス対策ソフトのパターンマッチングに似ています。
        
    - **メリット**: 既知の攻撃に対しては高い精度で検知・防御できます。誤検知が比較的少ないです。
        
    - **デメリット**: データベースに登録されていない**未知の攻撃（ゼロデイ攻撃）には対応できません**。常に最新のシグネチャに更新する必要があります。
        
2. **アノマリ型（Anomaly-based detection）**:
    
    - **仕組み**: 正常な通信パターンや振る舞いをあらかじめ学習し、それから逸脱した「異常な」通信を脅威と判断します。統計分析や機械学習が用いられます。
        
    - **メリット**: 未知の攻撃や、シグネチャにない巧妙な攻撃にも対応できる可能性があります。
        
    - **デメリット**: 正常な通信パターンを学習するのに時間がかかり、学習が不十分だと**誤検知（正常な通信を異常と判断）が多く発生する**可能性があります。逆に、正常な変動を許容しすぎて、異常を見逃す（過小検知）可能性もあります。
        

### IDS/IPSの配置場所と種類

IDS/IPSは、監視対象によって大きく2種類に分けられます。

- **NIDS/NIPS (Network-based IDS/IPS)**: ネットワーク上に配置され、ネットワーク全体を流れるパケットを監視します。外部からの攻撃だけでなく、内部からの不正な通信も検知可能です。
    
- **HIDS/HIPS (Host-based IDS/IPS)**: 個々のサーバーやPCなどのホストにソフトウェアとしてインストールされ、そのホストのシステムコール、ファイルアクセス、ログなどを監視します。
    

### [[次世代ファイアウォール（NGFW）]]との関係

最近では、IDS/IPSの機能は、前述の**次世代ファイアウォール（NGFW）**に統合されていることが一般的です。NGFWは、従来のファイアウォールの機能に加え、アプリケーション認識、[[SSL／TLSインスペクション]]、そして高度なIPS機能などを包括的に提供することで、より多層的な防御を実現します。これにより、別々にIDS/IPS製品を導入する手間が省け、セキュリティ管理の一元化が図られます。

### まとめ

IDS/IPSは、ファイアウォールが防ぎきれない、通信内容を悪用した攻撃や、システムの脆弱性を狙った攻撃などに対して有効なセキュリティ対策です。特にIPSは、自動で防御アクションを実行できるため、迅速な初動対応が求められる現代のサイバー攻撃において非常に重要な役割を担っています。