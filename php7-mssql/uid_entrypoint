#!/bin/sh
if ! whoami &> /dev/null; then
  if [ -w /etc/passwd ]; then
    echo "${USER_NAME:-container}:x:$(id -u):0:${USER_NAME:-container} user:${HOME}:/sbin/nologin" >> /etc/passwd
  fi
fi
exec "$@"
