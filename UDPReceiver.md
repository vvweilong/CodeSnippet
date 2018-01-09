    private DatagramSocket receiverSocket;
    private DatagramPacket receiverPacket;
    private byte[] recBuf;

    public UdpReceiver() {
        try {
    //            设置 监听的 端口号和 本地 ip
    //           receiverSocket= new DatagramSocket();
            receiverSocket = new DatagramSocket(12344, InetAddress.getLocalHost());
            recBuf = new byte[1024];
            receiverPacket = new DatagramPacket(recBuf, recBuf.length);

        } catch (SocketException e) {
            e.printStackTrace();
        } catch (UnknownHostException e) {
            e.printStackTrace();
        }
    }


    public void startListen() {
        new Thread(new Runnable() {
            @Override
            public void run() {
                int i = 0;
                while (i++ < 10) {
                    try {
                        Thread.sleep(200);
                        System.out.println("receiving packet");
                        receiverSocket.receive(receiverPacket);
                        System.out.println(new String(receiverPacket.getData(),"utf-8"));

                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    } catch (IOException e) {
                        e.printStackTrace();
                    }
                }
            }
        }).start();
    }