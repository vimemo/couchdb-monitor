FROM haproxy:1.8-alpine

RUN set -x	                            && \
	apk upgrade --update	                && \
	apk add bash ca-certificates rsyslog	&& \
	mkdir -p /etc/rsyslog.d/				      && \
	touch /var/log/haproxy.log				    && \
  # propagate rsyslogd writes to standard output of the container
	ln -sf /dev/stdout /var/log/haproxy.log

ADD ./etc/ /etc/
ADD ./entrypoint.sh /usr/local/bin/entrypoint
ENTRYPOINT [ "entrypoint" ]
CMD [ "-f", "/etc/haproxy.cfg" ]
