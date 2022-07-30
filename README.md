# Teleport 實作 bilbil 播放器效果

# 分析做法

1. 使用西瓜播放器建立播放器
   https://v2.h5player.bytedance.com/gettingStarted/#%E5%AE%89%E8%A3%85

2. 使用 Vue3 的 Teleport 建立傳送的內容

3. 使用 usevue 的 useIntersectionObserver 監聽播放器主區域是否在 viewport
