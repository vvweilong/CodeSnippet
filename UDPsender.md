     private DatagramSocket sendSocket;
    private DatagramPacket sendpacket;

    public UdpSender() {
        try {
            sendSocket = new DatagramSocket();
            String datastr = "this is from server";
            byte[] sendbuf = new byte[1024];
            sendpacket = new DatagramPacket(sendbuf, sendbuf.length);
            sendpacket.setData(datastr.getBytes("UTF-8"));
    //      设置发送方的 IP 为本机
            sendpacket.setAddress(InetAddress.getLocalHost());
    //      设置发送端口号为  12345
            sendpacket.setPort(12345);
            System.out.println("默认的 port :" + sendpacket.getPort());
            System.out.println("socket address : "+sendpacket.getSocketAddress().toString());

        } catch (SocketException e) {
            e.printStackTrace();
        } catch (UnknownHostException e) {
            e.printStackTrace();
        } catch (UnsupportedEncodingException e) {
            e.printStackTrace();
        }
    }

    public void startSend() {
        new Thread() {
            @Override
            public void run() {
                super.run();
                int i = 0;
                while (i++ < 10) {
                    try {
                        sleep(200);
                        System.out.println("sending packet");
                        sendSocket.send(sendpacket);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    } catch (IOException e) {
                        e.printStackTrace();
                    }
                }
            }
        }.start();
    }