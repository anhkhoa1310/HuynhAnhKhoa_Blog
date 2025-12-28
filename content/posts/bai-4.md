---
title: "Xử lý đa luồng cho Server Socket"
date: 2025-12-28
draft: false
tags: ["Multithread", "Optimization"]
summary: ""
---

Kỹ thuật đa luồng giúp Server xử lý nhiều Client đồng thời mà không bị nghẽn.

---

## 1. Mô hình xử lý


Mỗi kết nối sẽ được tách ra một Thread riêng để xử lý độc lập.