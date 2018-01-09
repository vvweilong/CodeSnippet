     @Override
        protected void onMeasure(int widthMeasureSpec, int heightMeasureSpec) {
            super.onMeasure(widthMeasureSpec, heightMeasureSpec);
            // Try for a width based on our minimum
            int minw = getPaddingLeft() + getPaddingRight() + getSuggestedMinimumWidth();
            int w = resolveSizeAndState(minw, widthMeasureSpec, 1);
            // Whatever the width ends up being, ask for a height that would let the pie
            // get as big as it can
            int minh = MeasureSpec.getSize(w) + getPaddingBottom() + getPaddingTop();
            int h = resolveSizeAndState(MeasureSpec.getSize(w), heightMeasureSpec, 0);
            setMeasuredDimension(w, h);
        }
         @Override
        protected void onSizeChanged(int w, int h, int oldw, int oldh) {
            super.onSizeChanged(w, h, oldw, oldh);
            float l = getPaddingLeft();
            float t = getPaddingTop();
            float r = w - getPaddingRight();
            float b = h - getPaddingBottom();
            //记录 绘制范围  考虑轮廓线的宽
            drawRect = new RectF(l, t, r, b);
            circleRadius = Math.min(drawRect.width(), drawRect.height()) * 0.5f;
            Log.i(TAG, "onSizeChanged: drawRect : " + drawRect.toString());
        }
    
