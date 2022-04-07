# ML_Class2
## General Guidance
### 如何做得更好？
 1. 先檢查training data的loss大小，看看model在training data上有沒有學起來
 2. 如何判對large loss是源於model bias or optimization？

           可以透過比較不同的模型來判斷現在的model夠不夠大！
           for testing data -> loss of 56 layers < loss of 20 layers
           for training data -> loss of 56 layers < loss of 20 layers 
           不是因為model bias跟overfitting, 而是optimization做得不夠好！
           
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

## When Gradient Is Small: Local Minimum and Saddle Point
### 如果optimization失敗的時候怎麼辦？
 1. Saddle point: gradient=0 but not local minima nor local maxima
 2. critical point: all points of gradient=0
    
    loss無法再下降是因為可能卡在critical point(有可能是在local minima or saddle point)
 3. Hessian不只可以告訴我們現在的critical point是否為saddle point，也能指出參數可以update的方向，而不用看gradient
 4. 在低維空間看起來是local minima，但在高維空間有可能就變成saddle point

## Tips for Training: Batch and Momentum
### 為什麼training的時候要用batch?
 1. 在分資料時會用shuffle，常見的作法是在每一個Epoch開始時重新分一次Batch
 2. 為什麼要用batch？
    
    large batch: 全部的資料當成一個batch，要把所有的資料看完才能計算loss跟gradient，才可update一次參數，較穩定
    
    small batch: batch size=1, 只要看一筆資料就能update一次參數，較不穩定（亂槍打鳥型）
    
    若考慮平行運算的話，large batch計算loss & gradient進而update參數所花的時間不一定比較長。
    
    但GPU的平行運算能力仍是有限，所以當batch size太大的時候，運算的時間還是會增加！
 3. Noisy gradient反而可以幫助training
 
    在兩個不同的模型上做實驗，發現在兩者上都是當Batch Size越大，training的結果越差。
    
    -> 同樣的模型，所以Function是一樣的，不是Model Bias問題
    
    -> 在Training上就有問題，所以不是Overfitting，是Optimization問題
    
    -> WHY?
    
    

     
     
