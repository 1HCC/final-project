猜數字遊戲 （Number Guessing Game）- Final Project 提案

專案簡介
這是一個基於FPGA的互動式猜數字遊戲，玩家需要根據提示在限定時間內輸入正確的數字組合。如果成功解答，將會顯示通關訊息並啟動蜂鳴器；若未在時間內完成，則顯示失敗訊息。

1.遊戲規則
-目標：
  在限定的時間內，使用開關（Switch）輸入正確的答案。
-輸入方式：
  玩家利用8位開關（p7~p0）組合出答案。
  每次按下check按鈕確認答案。
-判斷結果：
  如果答案正確，遊戲成功，顯示通關圖案(T)並啟動蜂鳴器。
  如果時間倒數到0仍未完成，遊戲失敗，顯示失敗圖案(F)。
-時間限制：
  倒數計時以秒為單位，由7段顯示器顯示剩餘時間。
  LED矩陣同時顯示遊戲狀態（成功或失敗）。

2.遊戲操作方式
-開機初始化：
  開啟電源後，FPGA會顯示初始化狀態（LED關閉，7段顯示器顯示時間倒數）。預設倒數時間為 59 秒。
-設定答案：
  遊戲的答案固定為 3 組8位二進制數字，可由程式內部設定或隨機生成（如：00000001、00010000、01011111）。
-輸入答案：
  玩家根據題目利用8個開關輸入答案，並按下check確認。
  程式將即時判斷是否正確並更新遊戲狀態。
-遊戲結束：
  若答案正確，LED矩陣顯示「通關」圖案，蜂鳴器響起。
  若倒數結束，LED矩陣顯示「失敗」圖案。

3.硬體設計與功能
-時鐘分頻模組（divfreq, divfreq2）：
  產生不同頻率的時鐘信號，用於控制倒數計時(1)及LED矩陣的刷新率(2)。
  
-LED矩陣顯示：
  透過8x8 LED矩陣呈現遊戲狀態，顯示通關或失敗的圖案。
  
  成功
  
  ![image](https://github.com/user-attachments/assets/5f62a032-0654-4960-8870-447803ee02c9)
  
  失敗
  
  ![image](https://github.com/user-attachments/assets/49657486-f165-412c-af65-a764172fac11)



-7段顯示器：
  用於顯示倒數計時（百位、十位、個位）。
  結合 BCD-to-7 段解碼模組實現動態顯示。
    ![image](https://github.com/user-attachments/assets/447ff8e4-68d8-4808-9fb7-fe5034fde18f)
  
-蜂鳴器控制：
  成功通關時，蜂鳴器發出聲音提示玩家。

![image](https://github.com/user-attachments/assets/e9e21271-928e-47ef-99d6-25ed6642d508)

-按鍵與開關輸入：
  8位開關用於輸入數字組合。
  按鍵（check）用於確認答案。
  按鍵 (reset) 用於重置遊戲。
  
  1~8為輸入數字 9為check 10為reset
  ![image](https://github.com/user-attachments/assets/da939fb8-2a88-44b2-8d54-21e3d4eb7525)


4.技術挑戰與學習成果
-分頻控制：
  學習如何生成精確的時鐘信號，並實現多模組同步運作。
-BCD轉7段顯示：
  理解BCD解碼及7段顯示的驅動邏輯，並應用於動態顯示切換。
-LED矩陣設計：
  透過陣列實現圖案切換與狀態顯示，增強遊戲的互動性。
-遊戲邏輯整合：
  設計符合遊戲規則的狀態機，實現正確的答案判斷與倒數計時。

5.操作展示流程
-開啟電源，LED矩陣與7段顯示器初始化。
-玩家輸入答案並按下check按鈕。
-若答案正確，蜂鳴器響起並顯示成功圖案；若答案錯誤，倒數計時繼續。
-時間倒數結束未正確輸入，顯示失敗圖案。


