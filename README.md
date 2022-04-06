# ML_Class2
## General Guidance
### 如何做得更好？
 1. 先檢查training data的loss大小，看看model在training data上有沒有學起來
 2. 如何判對large loss是源於model bias or optimization？

           可以透過比較不同的模型來判斷現在的model夠不夠大！
           for testing data -> loss of 56 layers < loss of 20 layers
           for training data -> loss of 56 layers < loss of 20 layers 
           不是因為model bias也不是overfitting, 而是optimization做得不夠好！
           
  3. Small loss on training data + large loss on testing data -> overfitting
 
     先去看loss on training data, 確認optimization沒有問題, 且model夠大了, 再去看loss on testing data
  4. Overfitting: 如果model自由度很高，就會產生非常奇怪的曲線，導致訓練資料上的loss小，但測試資料的loss大

     解決方法：
     
     (1) more training data
     
     (1.a) 尋找新的資料
     
     (1.b) data augmentation: 利用資料的特性、對問題的理解，來選擇適合的data augmentation的方式，創造出新的資料 （對現有資料做更動，變成新的資料）
     
     (2) 給model一些限制: 如已知trainging data的分布可能是二次曲線，那就將model限制在二次曲線的範圍
     
         若給model太多限制，會造成model bias
     
     (2.a) 如fully connected有較大的彈性，CNN則有一些限制，所以在影像辨識上處理得較佳
     
     (3) less features, early stopping, regularization, dropout 等
  
  5. 模型的複雜度與彈性
     
     複雜度：包含的function、參數比較多
     
  6. 如何選擇model？
     
     要把training set分成training set ＆ validation set
     
  7. 如何去分set？ N-fold cross validation
  
     Training set -> Train+Train+Val，分成三份，與model去做交叉驗證
    
  8. Mismatch
  
     一般的overfitting可以用收集更多的資料來克服，但mismatch卻是訓練資料跟測試資料分布是不一樣的，所以訓練資料再增加也沒有幫助！ 
     
     如何判斷是否為mismatch？ 根據對資料的理解，去看訓練資料與測試資料的方式，才能判斷是否為mismatch
     
     
