<!-- loioff51a3258fe54c308c05ed5901d1a793 -->

# Secure Development in the Kyma Environment

Secure development focuses on Pod security, network traffic restriction, Istio sidecar proxy injection, and workload exposure. Learn about the security measures you can take.



<a name="loioff51a3258fe54c308c05ed5901d1a793__section_z3k_bbj_ybc"/>

## Pod Security

Read [Kubernetes Pod Security Recommendations](kubernetes-pod-security-recommendations-f8cb6e5.md) for details on how to secure your Kubernetes Pods in Kyma.



<a name="loioff51a3258fe54c308c05ed5901d1a793__section_dhq_gbj_ybc"/>

## Restrict and Secure Network Traffic

-   Set up Kubernetes [Network Policies](https://kubernetes.io/docs/concepts/services-networking/network-policies/) to restrict the network traffic between Pods in your namespaces

-   [Enable Automatic Istio Sidecar Proxy Injection](https://kyma-project.io/#/istio/user/operation-guides/02-20-enable-sidecar-injection) for your namespaces




<a name="loioff51a3258fe54c308c05ed5901d1a793__section_bwc_zbj_ybc"/>

## Expose Workloads Securely

To securely expose workloads in SAP BTP, Kyma runtime, use the Istio and API Gateway modules. As a prerequisite, make sure that you have those two modules added to your Kyma cluster. Then you can follow steps from these tutorials:

-   [Set Up a Custom Domain for a Workload](https://kyma-project.io/#/api-gateway/user/tutorials/01-10-setup-custom-domain-for-workload)

-   [Disable the default Gateway](https://kyma-project.io/#/api-gateway/user/custom-resources/apigateway/04-10-kyma-gateway?id=disable-or-enable-kyma-gateway)

-   Set up your own API Gateway

    -   with TLS. See [Set Up a TLS Gateway in Simple Mode](https://kyma-project.io/#/api-gateway/user/tutorials/01-20-set-up-tls-gateway)

    -   with mTLS. See [Set Up an mTLS Gateway and Expose Workloads Behind It](https://kyma-project.io/#/api-gateway/user/tutorials/01-30-set-up-mtls-gateway)


-   Create an [APIRule Custom Resource](https://kyma-project.io/#/api-gateway/user/custom-resources/apirule/04-10-apirule-custom-resource) to securely expose your workloads

    -   [Expose and Secure a Workload with JWT](https://kyma-project.io/#/api-gateway/user/tutorials/01-50-expose-and-secure-a-workload/01-52-expose-and-secure-workload-jwt)

    -   [Expose and Secure a Workload with Istio](https://kyma-project.io/#/api-gateway/user/tutorials/01-50-expose-and-secure-a-workload/01-53-expose-and-secure-workload-istio)

    -   [Expose and Secure a Workload with a Certificate](https://kyma-project.io/#/api-gateway/user/tutorials/01-50-expose-and-secure-a-workload/01-54-expose-and-secure-workload-with-certificate)





<a name="loioff51a3258fe54c308c05ed5901d1a793__section_qfk_t2j_ybc"/>

## Module-Specific Security Considerations



### Serverless Module

See [Security Considerations](https://kyma-project.io/#/serverless-manager/user/00-40-security-considerations) for the Serveless module.

**Related Information**  


[Kyma Security Concepts](kyma-security-concepts-dbf4503.md "SAP BTP, Kyma runtime takes various security measures regarding your cluster and its underlying infrastructure. Benefit from the security setup that SAP BTP, Kyma runtime provides.")

[Secure Administration and Operations in the Kyma Environment](secure-administration-and-operations-in-the-kyma-environment-a22ef28.md "Secure administration and operations focus on landscape setup, authentication, authorization, and Istio access logs. Learn about the security measures you can take from the following sections.")

[Kubernetes Pod Security Recommendations](kubernetes-pod-security-recommendations-f8cb6e5.md " 		 	")

[Function Security](function-security-1be599b.md "When creating Functions, make sure you understand how they work to avoid potential threats.")

