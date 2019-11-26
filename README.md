# jaeger-web-java 简介

## 简介
jaeger-web-java 的目标是实现 Java 服务间链路追踪。对 [java-spring-web](https://github.com/opentracing-contrib/java-spring-web)项目做了进一步开发，
jaeger-web-java 会从 nginx 发出的 request 中获取 requestID 并且作为 tag 放在 tracer 中，
可以在 jaeger UI 中通过查询 `request-id=?` 获取对应的链路信息。

## 使用
### pom.xml
```xml
<dependency>
	<groupId>com.zzcrowd</groupId>
	<artifactId>opentracing-jaeger</artifactId>
	<version>0.0.1-SNAPSHOT</version>
</dependency>
```
### deployment.yaml
```yaml
JAEGER_SAMPLER_TYPE
JAEGER_SAMPLER_PARAM
SERVICE_NAME
NODE_IP
```
##### JAEGER_SAMPLER_TYPE 采样类型
1. const

2. probabilistic

##### JAEGER_SAMPLER_PARAM 采样率
当 type 为 `const` 时，可取值为 0 和 1，0 为不采样，1为全采样。
当 type 为 `probabilistic` 时，可取值 为 0~1。

##### SERVICE_NAME 服务名
与 labels.app 相同
##### NODE_IP 节点 IP
插入方式：
```yaml
- name: NODE_IP
  valueFrom:
    fieldRef:
      fieldPath: status.hostIP
```



