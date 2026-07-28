# ngx_http_smemcached

include $(dir $(abspath $(lastword $(MAKEFILE_LIST))))/version

PKGS += ngx_http_smemcached

$(TARBALLS)/ngx_http_smemcached-$(NGX_HTTP_SMEMCACHED_VERSION).tar.gz:
	$(true)

.sum-ngx_http_smemcached: ngx_http_smemcached-$(NGX_HTTP_SMEMCACHED_VERSION).tar.gz

ngx_http_smemcached: ngx_http_smemcached-$(NGX_HTTP_SMEMCACHED_VERSION).tar.gz .sum-ngx_http_smemcached
	$(UNPACK)
	$(MOVE)

.ngx_http_smemcached: ngx_http_smemcached
	touch $@
