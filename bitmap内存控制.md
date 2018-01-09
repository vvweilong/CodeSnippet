    /**
     * 仅仅是从采样率上进行缩放
     *
     * @param targetH 目标显示区域的高度
     * @param targetW 目标显示区域的宽度
     */
    private Bitmap scaleImage(int targetW, int targetH) {
        //创建 option 对象 用于参数设置 以及 信息装载
        BitmapFactory.Options options = new BitmapFactory.Options();
        //设置 为 只获取图片信息
        options.inJustDecodeBounds = true;
        Bitmap boundBitmap = BitmapFactory.decodeResource(getResources(), R.drawable.test, options);
        //获取图片原始尺寸
        int originW = options.outWidth;
        int originH = options.outHeight;
        //判断 显示比例与原图像比例是否一致 不一致 采用最大的缩放比率 保证图片全部显示出来
        int scaleRatio = Math.max(originH / targetH, originW / targetW);
        options.inSampleSize = scaleRatio;
        Log.i(TAG, "scaleImage: ratio = " + scaleRatio);
        options.inJustDecodeBounds = false;
        boundBitmap = BitmapFactory.decodeResource(getResources(), R.drawable.test, options);
        Log.i(TAG, "scaleImage: bitmap size " + byteSize2Str(boundBitmap.getByteCount()));
        return boundBitmap;
    }
    
          /**
         * 从颜色模式 也就是表示一个像素颜色所用的字节数进行压缩优化
         */
        private Bitmap optimizeFormat() {
            //创建 option 对象
            BitmapFactory.Options options = new BitmapFactory.Options();
            //采用占用字节最低的颜色模式来渲染图片  
    //        options.inPreferredConfig = Bitmap.Config.RGB_565; 2个字节
    //        options.inPreferredConfig = Bitmap.Config.ALPHA_8; 2个字节
    //        options.inPreferredConfig = Bitmap.Config.ARGB_4444; 4个字节
            options.inPreferredConfig = Bitmap.Config.ARGB_8888; 8个字节
            Bitmap boundBitmap = BitmapFactory.decodeResource(getResources(), R.drawable.test, options);
            Log.i(TAG, "scaleImage: bitmap size " + byteSize2Str(boundBitmap.getByteCount()));
            return boundBitmap;
        }
