---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 應用程式詳細資料
{: #manageapps}

{{site.data.keyword.Bluemix}} 主控台中的「應用程式」儀表板提供您所建立之應用程式的摘要資訊。摘要資訊包括應用程式的名稱、圖示、URL、運行環境及執行狀態，以及連結至應用程式的服務實例。
{:shortdesc}

從「應用程式」儀表板中，您可以檢視每一個應用程式的狀態。

**已停止或不明（灰色）**

  您的應用程式已停止，或狀態不明。灰色圖示表示應用程式已停止，或狀態不明。

**執行中（綠色）**

  您的應用程式正在執行中。綠色圖示表示應用程式已啟動，且所有實例都在執行中。

*數字* **執行中（黃色）**

  應用程式已啟動，但並非所有實例都在執行中。黃色圖示表示少於 100% 的實例正在執行中。會顯示執行中的實例數和失敗的實例數。

**不在執行中（紅色）**

  您的應用程式不在執行中。紅色圖示表示應用程式已啟動，但沒有任何實例在執行中。

若要檢視應用程式的相關資訊，請按一下名稱，以開啟應用程式的「概觀」頁面。

部署應用程式時，您可以啟動、停止、重新啟動或（如果是 Web 應用程式）修改實例數及應用程式所使用的記憶體量。目前對於 Web 應用程式，{{site.data.keyword.Bluemix_notm}} 並不會根據其負載自動擴充應用程式，因此，您必須自行管理這個層面。

如果發生更新，則可以重新部署應用程式。用於更新應用程式的機制是一開始用來部署它的相同機制。{{site.data.keyword.Bluemix_notm}} 會停止所有執行中的實例，並自動將其取代成新的實例。
