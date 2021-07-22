#### 各 Tab Bar View Cycle
- 首次出現時，會執行 viewDidLoad:首次顯示畫面時，會進行記憶體分配。
- 在viewDidLoad初使化的程式，離開後再回來，會和之前一樣。
- 若在viewWillAppear進行初始化，回來後會重置。
- 由於記憶體不會被釋放，故設計畫面太過複雜時，需要加入didReceiveMemoryWarning來釋放記憶體。
