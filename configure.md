# 작업할 클라우드 컴퓨트 인스턴스 생성 및 접속

작업할 인스턴스를 생성하고 접속을 하는 단계입니다.

1. public subnet 생성
1. public subnet 으로 compute instance 생성

# Putty로 인스턴스에 접속

1. **Session** 구역에서 compute instance의 public ip와 포트를 설정합니다.

    ![Alt text](https://monosnap.com/image/cR9kYm4eJ6NE4PyEMEWKBq83twnt7v)

1. **Connection > SSH > Auth** 구역에서 ppk 파일 위치를 설정합니다.

    ![Alt text](https://monosnap.com/image/xG5sAAcQX3LUBQRZWcxNyoaa7FdLGA)

1. 하단부의 **Open**을 눌러 인스턴스에 접속합니다.

    접속된 후 login as : 부분에 **opc** 를 입력하면 로그인 됩니다.

    ![Alt text](https://monosnap.com/image/8wzSgnHSblJK6TFLrrYu8GnnEMmVS7)


그 외 다른 터미널 에뮬레이터나 ssh 로 접속 가능합니다.


# docker 설치
1. docker가 있는지 검사합니다.
    ~~~
    docker
    ~~~

1. docker를 설치합니다.
    ~~~
    sudo yum install -y docker-eingine
    ~~~

1. docker를 시작합니다.
    ~~~
    sudo systemctl start docker
    sudo systemctl enable docker
    ~~~

1. 확인합니다.
    ~~~
    sudo docker ps
    ~~~

# kubectl 설치

1. kubectl이 있는지 검사합니다.
    ~~~
    kubectl
    ~~~

1. kubectl을 설치합니다.
    ~~~
    sudo yum install -y kubectl
    ~~~


# OCI cli 설치
1. cli를 설치합니다.
    ~~~
    bash -c "$(curl -L https://raw.githubusercontent.com/oracle/oci-cli/master/scripts/install/install.sh)"
    ~~~

    프롬프트로 질문사항이 나오면 Enter 만 계속 누릅니다.

1. 현재 터미널에 환경을 적용합니다.
    ~~~
    . ./.bashrc
    ~~~

1. 설정을 합니다.
    ~~~
    oci setup config
    ~~~

    입력해야 할 부분은 다음과 같습니다.

    - Enter a user OCID: 
    
        user OCID 값은 User Settings(사용자 설정) 화면의 중간에 User Information(사용자 정보) 항목에 있습니다. Copy(복사) 버튼을 누르면 복사됩니다.

        ![Alt text](https://monosnap.com/image/gkdtW4CtFczlStGEEFdanFslpXjMC2)
        
        ![Alt text](https://monosnap.com/image/hHeiTFINWPKQyK8QkwYq1JECtoct5k)
        
    - Enter a tenancy OCID: 
    
        tenancy OCID 값은 태넌시 정보 화면의 중간에 Tenancy Information(태넌시 정보) 항목에 있습니다. Copy(복사) 버튼을 누르면 복사됩니다.

        ![Alt text](https://monosnap.com/image/TN3SkTUcXpABGQjylj5HX7KP7fHUBp)

        ![Alt text](https://monosnap.com/image/sEdvv02yE1h5Pa9BEI5jldsXvcioTO)
    
    - Enter a region (e.g. eu-frankfurt-1, uk-london-1, us-ashburn-1, us-phoenix-1): 
        region은 상단 우측에 존재합니다.

        ![Alt text](https://monosnap.com/image/qcV8dVveQKnHLX7BMIkFfP2c4uiEDE.png)


    나머지 key 에 해당하는 부분은 Enter 만 입력하도록 합니다.

# 생성된 공개키 등록

위의 항목에서 실행한 **oci setup config** 명령에서 새로운 키를 생성을 하였습니다. OCI를 통해서 명령을 하려면 이 키를 클라우드에 등록을 해야 합니다.

1. 공개키 값을 복사합니다.

    ~~~
    cd ~/.oci
    cat oci_api_key_public.pem
    ~~~

    ![Alt text](https://monosnap.com/image/65J2zUjxHeFsbGIa4WFlslUWa3kfLo)

    **-----BEGIN PUBLIC KEY-----** 부터 **-----END PUBLIC KEY-----** 까지 모두 복사합니다.

1. 사용자 세부정보를 봅니다.

    ![Alt text](https://monosnap.com/image/gkdtW4CtFczlStGEEFdanFslpXjMC2)

1. 아래의 **공개키 추가** 를 선택합니다.

    ![Alt text](https://monosnap.com/image/3dgQKEL64vwOXNGo4EmXWddWcK02Po)

1. 좀 전에 복사한 공개키 값을 붙여넣기하고 **추가**를 누릅니다.

    ![Alt text](https://monosnap.com/image/VCizZtagNrjc4qgcxUBlk161JqMxUx)

1. 잘 동작하는지 체크합니다.

    ~~~
    oci os ns get
    ~~~

    오류가 나지 않고 값이 나오면 설정이 완료되었습니다.

# kubeconfig 설정
1. 다음 작업을 완료했는지 확인하십시오. 위의 내용을 완료하였으면 다음 작업으로 넘어갑니다.
    - API 서명 키 쌍을 생성했습니다. 
    - API 서명 키 쌍의 공개 키 값을 사용자 이름의 사용자 설정에 추가했습니다.
    - Oracle Cloud Infrastructure CLI를 설치 및 구성했습니다.
    
    위의 작업 중 하나 이상을 수행하지 않았거나 확실하지 않은 경우, Kubernetes 설명서의 Container Engine에서 [kubeconfig 파일을 다운로드하여 클러스터 액세스를 활성화하는 방법](https://docs.cloud.oracle.com/iaas/Content/ContEng/Tasks/contengdownloadkubeconfigfile.htm) 항목을 참조하십시오.

1. 개발자 서비스 > 컨테이너 클러스터(OKE)를 선택하고, 이전에 만들었던 클러스터를 선택합니다.
    
    ![Alt text](https://monosnap.com/image/AsXRAKoBcYWLnVnb7N0OcrIRcoq7GX)

1. `Kube Cluster`에 대한 세부 정보가 표시된 클러스터 페이지에서 Access Kubeconfig를 클릭하여 Kubeconfig 액세스 방법 대화 상자를 표시합니다.

    ![Alt text](https://monosnap.com/image/vhd4fUiyL5yZPJLsjH1IEOTxO8FwE6.png)

1. 화면에 나온 명령어를 복사하여 터미널에서 실행합니다.

    ~~~sh
    $ mkdir -p $HOME/.kube
    $ oci ce cluster create-kubeconfig --cluster-id ocid1.cluster.oc1.phx.aaaaaaaaae ... --file $HOME/.kube/config --region us-ashburn-1
    ~~~

    여기서 `ocid1.cluster.oc1.phx.aaaaaaaaae ...`는 현재 클러스터의 OCID입니다. 편의상 Kubeconfig 액세스 방법 대화 상자의 명령에 이미 클러스터의 OCID가 포함되어 있습니다.

1. 만들어진 환경을 적용합니다.

    ~~~
    export KUBECONFIG=$HOME/.kube/config
    ~~~

1. 닫기를 클릭하여 Kubeconfig 액세스 방법 대화 상자를 닫습니다.


# kubectl 및 Kubernetes 대시 보드에 대한 클러스터 액세스 확인

1. kubectl을 이미 설치했는지 확인하십시오. 아직 수행하지 않았다면, [kubectl 문서](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl)를보십시오.

1. kubectl을 사용하여 생성 한 새 클러스터에 연결할 수 있는지 확인하십시오. 터미널 창에서 다음 명령을 입력하십시오.
    
    ~~~sh
    $ kubectl cluster-info
    ~~~
    
    ![Alt text](https://monosnap.com/image/Nu2zju3BiZoOIWLWI51IehLRvNAOWa)
    
<!--
# 방화벽 설정
~~~
firewall-cmd --add-masquerade --permanent
firewall-cmd --add-port=10250/tcp --permanent
firewall-cmd --add-port=8472/udp --permanent
firewall-cmd --add-port=6443/tcp --permanent
~~~
-->