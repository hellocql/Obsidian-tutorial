        /// <summary>  
        /// ScreenPointToLocalPointInRectangle 的 event 相机须与目标 Rect 所在 Canvas 的 RenderMode 一致（见 CameraUtils 注释）。  
        /// </summary>  
        private static Camera GetEventCameraForRect(RectTransform parent)  
        {  
            if (parent == null)  
                return null;  
  
            var canvas = parent.GetComponentInParent<Canvas>();  
            if (canvas == null)  
                return CameraUtils.UICamera;  
  
            if (canvas.renderMode == RenderMode.ScreenSpaceOverlay)  
                return null;  
  
            if (IsCameraValid(canvas.worldCamera))  
                return canvas.worldCamera;  
  
            return CameraUtils.UICamera;  
        }