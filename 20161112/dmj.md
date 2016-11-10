#cookie_collector.py  

쿠키 값을 [id, domain, cookie, captured_time]의 스키마로 구성하여  
result.db에 저장하는 프로그램을 작성하였습니다.

#plug-in_handler.py

멀티프로세싱으로 개발한 플러그인들(kakao_sniffer, naver_mail_sniffer, dns_sniffer, cookie_collector)을  
하나의 파이썬 소스로 실행하게끔 하는 plug-in_handler.py 를 작성하였습니다.  
아직 성능이나 메모리 상의 이슈가 존재할 것이라 생각하여 수정방안을 모색중입니다.  