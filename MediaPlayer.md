    /**
    * 在 BluetoothA2DP 可以播放
    * 在 BluetoothHeadset 情况下也可以播放
    *
    */
    
    private MediaPlayer mediaPlayer;

    private void stopPlayMedia() {
        Log.i(TAG, "stopPlayMedia: ");
        if (mediaPlayer != null) {
            if (mediaPlayer.isPlaying()) {
                mediaPlayer.pause();
                mediaPlayer.stop();
            }
        }
    }

    private void startPlayMedia(Uri uri)  {
        Log.i(TAG, "startPlayMedia: ");
        mediaPlayer = new MediaPlayer();
        mediaPlayer.setOnPreparedListener(new MediaPlayer.OnPreparedListener() {
            @Override
            public void onPrepared(MediaPlayer mp) {
                mp.seekTo(0);
                mp.start();
            }
        });
        try {
            mediaPlayer.setDataSource(this, uri);
            mediaPlayer.prepare();

        } catch (IOException e) {
            e.printStackTrace();
        }
    }