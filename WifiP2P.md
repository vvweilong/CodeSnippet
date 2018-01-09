    
    //init
    wifiP2pManager = (WifiP2pManager) getSystemService(WIFI_P2P_SERVICE);

    channel = wifiP2pManager.initialize(this, Looper.getMainLooper(), new WifiP2pManager.ChannelListener() {
            @Override
            public void onChannelDisconnected() {
                Log.i(TAG, "onChannelDisconnected: ");
            }
        });
        
    //broadcast receiver
    private BroadcastReceiver wifip2pReceiver = new BroadcastReceiver() {
        @Override
        public void onReceive(Context context, Intent intent) {
            String action = intent.getAction();
            Log.i(TAG, "onReceive: action " + action);
            if (WifiP2pManager.WIFI_P2P_STATE_CHANGED_ACTION.equals(action)) {
                // Check to see if Wi-Fi is enabled and notify appropriate activity
            } else if (WifiP2pManager.WIFI_P2P_PEERS_CHANGED_ACTION.equals(action)) {
                // Call WifiP2pManager.requestPeers() to get a list of current peers
                if (wifiP2pManager != null) {
                    Log.i(TAG, "onReceive: peers changed");
                    wifiP2pManager.requestPeers(channel, peerListListener);
                }

            } else if (WifiP2pManager.WIFI_P2P_CONNECTION_CHANGED_ACTION.equals(action)) {
                // Respond to new connection or disconnections
            } else if (WifiP2pManager.WIFI_P2P_THIS_DEVICE_CHANGED_ACTION.equals(action)) {
                // Respond to this device's wifi state changing
            }
        }
    };
    
    //discover
     wifiP2pManager.discoverPeers(channel, new WifiP2pManager.ActionListener() {
                    @Override
                    public void onSuccess() {
                        Log.i(TAG, "onSuccess: discover peers");
                    }

                    @Override
                    public void onFailure(int reason) {
                        Log.i(TAG, "onFailure: ");
                    }
                });
                handler.postDelayed(new Runnable() {
                    @Override
                    public void run() {
                        wifiP2pManager.stopPeerDiscovery(channel, new WifiP2pManager.ActionListener() {
                            @Override
                            public void onSuccess() {
                                Log.i(TAG, "onSuccess: stop peer discover");
                            }

                            @Override
                            public void onFailure(int reason) {

                            }
                        });
                    }
                }, 10000);