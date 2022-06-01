# travis-ci-deploy

Nginx, SpringBoot, CodeDeploy, Travis CI를 이용한 무중단 배포 시스템입니다.   
AWS의 EC2, S3, CodeDeploy, IAM 서비스를 사용했습니다. 자세한 구현 방법은 밑의 글을 참고하시면 됩니다.   

## 구현 방식에 대한 설명 
1. [Travis CI와 AWS CodeDeploy를 사용한 자동배포 구축하기 #1](https://develop-writing.tistory.com/122)
2. [Travis CI와 AWS CodeDeploy를 사용한 자동배포 구축하기 #2](https://develop-writing.tistory.com/123)
3. [무중단 배포 시스템 만들기](https://develop-writing.tistory.com/124)

## 무중단 배포 전체 구조
![68747470733a2f2f74312e6461756d63646e2e6e65742f6366696c652f746973746f72792f393936463736334435413733463931453236](https://user-images.githubusercontent.com/68800994/171329797-6bbacba0-0ca7-4842-95bf-13e212525c82.png)

## 배포 과정
1. 개발 이후 main 브런치에 Push를 합니다.
2. Travis CI에서 프로젝트 Test 및 Build를 진행합니다.
   <img width="1010" alt="스크린샷 2022-05-28 오후 5 33 26" src="https://user-images.githubusercontent.com/68800994/171333039-fc83f041-ee5d-44e5-a08c-3e80d5cc9c4f.png">
4. 2번이 성공하면 지정된 이메일에 빌드 성공 메일을 보냅니다.
   <img width="993" alt="image" src="https://user-images.githubusercontent.com/68800994/171331701-3c51b00b-fed0-46f7-8595-a3ec94f6f5ec.png">
5. Travis CI에서 빌드 결과물을 S3에 저장합니다.(jar 파일과 배포할 때 필요한 쉘 파일들)
   <img width="1156" alt="스크린샷 2022-06-01 오후 1 42 54" src="https://user-images.githubusercontent.com/68800994/171331587-21a35a9f-7f9c-4d60-a922-e2e6cc04eab5.png">
   <img width="350" alt="스크린샷 2022-06-01 오후 1 53 27" src="https://user-images.githubusercontent.com/68800994/171331553-e637f910-19e6-4109-8e7b-7dcd0d9833de.png">
6. AWS CodeDeploy에서 S3에 저장된 빌드 결과물을 가지고 EC2에 배포를 진행합니다. 
  <img width="887" alt="스크린샷 2022-06-01 오후 1 43 45" src="https://user-images.githubusercontent.com/68800994/171331573-555cc9c8-1085-4469-998a-837871a4bf96.png">
  <img width="506" alt="스크린샷 2022-06-01 오후 1 44 04" src="https://user-images.githubusercontent.com/68800994/171331539-a985e454-acee-4622-943b-b27ea7eb6a36.png">
