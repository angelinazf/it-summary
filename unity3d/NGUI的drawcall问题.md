### 导入下列patch
```
diff --git a/Assets/NGUI/Scripts/Internal/UIWidget.cs b/Assets/NGUI/Scripts/Internal/UIWidget.cs
index 884ab73..f95a005 100755
--- a/Assets/NGUI/Scripts/Internal/UIWidget.cs
+++ b/Assets/NGUI/Scripts/Internal/UIWidget.cs
@@ -427,8 +427,8 @@ static public int CompareFunc (UIWidget left, UIWidget right)
 			Material rightMat = right.material;
 
 			if (leftMat == rightMat) return 0;
-			if (leftMat != null) return -1;
-			if (rightMat != null) return 1;
+			if (leftMat == null) return 1;
+			if (rightMat == null) return -1; 
 			return (leftMat.GetInstanceID() < rightMat.GetInstanceID()) ? -1 : 1;
 		}
 		return val;
```