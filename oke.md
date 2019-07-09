# OCI (Oracle Cloud Infrastructure) 시작하기
1. 브라우저에서 Oracle Cloud Infrastructure에 로그인하기 위해 제공 한 URL로 이동하십시오. (예: https://console.us-ashburn-1.oraclecloud.com/)

   ![Tenant](https://image.prntscr.com/image/05I_oK2xTJCbV6dysxS_OQ.png)

1. Tenant명에는 제공된 명을 입력합니다.

   ![login](https://image.prntscr.com/image/n4ZodMHLSFK8nC5oRSmD3g.png)

1. 클러스터를 만들 수있는 적절한 권한이있는 임차인을 지정하십시오. 다음 권한 중 하나를 사용하여 이러한 사용 권한을 상속합니다.
    - 임차인의 관리자 그룹에 속함
    - 정책이 Kubernetes 사용 권한을위한 적절한 컨테이너 엔진과 VCN_READ 및 SUBNET_READ 네트워킹 사용 권한을 부여하는 다른 그룹에 속함
1. 사용자 이름과 암호를 입력하십시오.

# 리소스 제어권한 부여하기
Kubernetes를 설정하기 위해서는 권한을 부여해야 합니다.

1. 왼쪽 상위의 MENU를 누르고 Identy 항목의 Policies 를 선택합니다.

   ![Policies 선택](https://image.prntscr.com/image/X0n6zTtbT-GARx9EYo-EAw.png)
    
1. COMPARTMENT 아래 메뉴를 눌러 (root) 라고 표기된 compartment를 선택합니다.

   ![compartment 선택](https://image.prntscr.com/image/gH_TWTO2QMywpI6Ap8XQjw.png)

1. Create Policy 버튼을 클릭하여 새로운 Policy를 만듭니다.

   ![Policy 생성](https://image.prntscr.com/image/ZF8vpamuSl_sf2FgloIxVw.png)

1. NAME을 쓰고(예:oke-service) STATEMENT에 "`allow service OKE to manage all-resources in tenancy`" 라고 입력합니다.

   ![STATEMENT 입력](https://image.prntscr.com/image/xfkQfzYHRz60toO01zjKGw.png)

저장을 하면 Kubernetes 클러스터링을 만들 수 있는 권한이 부여가 되었습니다.

# Kubernetes Cluster 생성하기

1. OKE 관리화면으로 들어갑니다.

    **개발자 서비스 > 컨테이너 클러스터(OKE)** 를 눌러 클러스터 관리화면을 보여줍니다.

    ![Alt text](https://monosnap.com/image/Q3VaaKATIJmt24DKvQfrJalagsLLCl)

1. **클러스터 생성** 버튼을 클릭합니다.

    ![Alt text](https://monosnap.com/image/X0OxxuuNq3BkHZDyqgps3utYy8LVjk)

1. **생성** 을 클릭하여 클러스터를 만듭니다.

    ![Alt text](https://monosnap.com/image/gIehPYWvJPXCJeB72fvjXSTVx44jPE)