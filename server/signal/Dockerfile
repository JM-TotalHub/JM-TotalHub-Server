# STUN/TURN 서버용 Dockerfile
FROM coturn/coturn:latest

# 루트 사용자로 전환
USER root

# gettext 패키지 설치
RUN apt-get update && apt-get install -y gettext && rm -rf /var/lib/apt/lists/*

# 다시 일반 사용자로 전환 (필요한 경우)
# USER turnserver

# 기본 설정 파일 복사
COPY /server/signal/turnserver.conf.template /etc/turnserver.conf.template

RUN cat /etc/turnserver.conf.template

# 필요한 ARG 정의
ARG ICE_SERVER_LISTENING_IP
ARG ICE_SERVER_EXTERNAL_IP
ARG ICE_SERVER_PORT
ARG ICE_SERVER_MIN_PORT
ARG ICE_SERVER_MAX_PORT
ARG ICE_SERVER_REALM
ARG ICE_SERVER_USER

# ARG를 ENV로 설정
ENV ICE_SERVER_LISTENING_IP=${ICE_SERVER_LISTENING_IP}
ENV ICE_SERVER_EXTERNAL_IP=${ICE_SERVER_EXTERNAL_IP}
ENV ICE_SERVER_PORT=${ICE_SERVER_PORT}
ENV ICE_SERVER_MIN_PORT=${ICE_SERVER_MIN_PORT}
ENV ICE_SERVER_MAX_PORT=${ICE_SERVER_MAX_PORT}
ENV ICE_SERVER_REALM=${ICE_SERVER_REALM}
ENV ICE_SERVER_USER=${ICE_SERVER_USER}

# 환경변수 내용 확인
RUN echo "ICE_SERVER_LISTENING_IP=${ICE_SERVER_LISTENING_IP}" && \
    echo "ICE_SERVER_EXTERNAL_IP=${ICE_SERVER_EXTERNAL_IP}" && \
    echo "ICE_SERVER_PORT=${ICE_SERVER_PORT}"

# 도커파일 환경변수 등록
ENV ICE_SERVER_LISTENING_IP=${ICE_SERVER_LISTENING_IP}
ENV ICE_SERVER_EXTERNAL_IP=${ICE_SERVER_EXTERNAL_IP}
ENV ICE_SERVER_PORT=${ICE_SERVER_PORT}
ENV ICE_SERVER_MIN_PORT=${ICE_SERVER_MIN_PORT}
ENV ICE_SERVER_MAX_PORT=${ICE_SERVER_MAX_PORT}
ENV ICE_SERVER_REALM=${ICE_SERVER_REALM}
ENV ICE_SERVER_USER=${ICE_SERVER_USER}

# 설정 파일 생성
RUN envsubst < /etc/turnserver.conf.template > /etc/turnserver.conf

RUN cat /etc/turnserver.conf

# TURN 서버 실행 명령
# CMD ["turnserver", "-c", "/etc/turnserver.conf"]
