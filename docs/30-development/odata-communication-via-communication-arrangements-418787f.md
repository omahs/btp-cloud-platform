<!-- loio418787f81805485f993ce21d15152092 -->

# OData Communication via Communication Arrangements

OData outbound communication can be established using so-called communication arrangements.



<a name="loio418787f81805485f993ce21d15152092__prereq_mb5_vqx_kzb"/>

## Prerequisites

-   You've created a communication scenario as described in [Defining a Communication Scenario Including Authorization Values](defining-a-communication-scenario-including-authorization-values-bba0fd2.md).
-   You have a service meta data file \(EDMX file\) for the service you want to consume.
-   You have created and activated a service consumption model \(SRVC\) of type `OData`. See [Creating Service Consumption Model](https://help.sap.com/docs/abap-cloud/abap-development-tools-user-guide/creating-service-consumption-model?version=sap_btp) for more information.



## Procedure

1.  Create a corresponding outbound service of type HTTP.

    1.  In your ABAP project, select the relevant package node in the Project Explorer.

        Open the context menu and choose *File* \> *New* \> *Other* \> *ABAP Repository Object* \> *Cloud Communication Managemengt* \> *Outbound Service* \> *Next* to launch the creation wizard.

    2.  Select *HTTP Service* in the *Service Type* dropdown list.

    3.  Choose Next and select a transport request.

    4.  Optional: Go to your outbound service and enter the URL in the field *Default Path Prefix*.
    5.  Save the outbound service.


2.  Add the newly created outbound service to a communication scenario. See [Service Consumption via Communication Arrangements](service-consumption-via-communication-arrangements-86aece6.md) for more information.

3.  Publish the communication scenario. The administrator can then create the required communication management objects as described in [Next Steps](odata-communication-via-communication-arrangements-418787f.md#loio418787f81805485f993ce21d15152092__postreq_cq3_ctx_kzb).

4.  Call the OData service as described in the example. Copy the code snippet from the *Overview* tab in your SRVC and add the `comm_system_id` and `service_id` parameters if necessary. According to your developed communication scenario, add the following:


    <table>
    <tr>
    <td valign="top">
    
    `comm_scenario`
    
    </td>
    <td valign="top">
    
    mandatory
    
    </td>
    <td valign="top">
    
    ID of the developed communication scenario
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    `comm_system_id`
    
    </td>
    <td valign="top">
    
    optional
    
    </td>
    <td valign="top">
    
    ID of the configured communication system
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    `service_id`
    
    </td>
    <td valign="top">
    
    optional
    
    </td>
    <td valign="top">
    
    ID of the developed outbound service
    
    </td>
    </tr>
    </table>
    



## Example

The following code is generated by the SRVC for the create operation of the OData service `Business User`.

> ### Sample Code:  
> ```
> 
> DATA:
>   ls_business_data TYPE business_user=>tys_users,
>   lo_http_client   TYPE REF TO if_web_http_client,
>   lo_client_proxy  TYPE REF TO /iwbep/if_cp_client_proxy,
>   lo_request       TYPE REF TO /iwbep/if_cp_request_create,
>   lo_response      TYPE REF TO /iwbep/if_cp_response_create.
> 
> 
> TRY.
> * Create http client
> DATA(lo_destination) = cl_http_destination_provider=>create_by_comm_arrangement(
> *                                             comm_scenario  = '<Comm Scenario>'
> *                                             comm_system_id = '<Comm System Id>'
> *                                             service_id     = '<Service Id>' ).
> *lo_http_client = cl_web_http_client_manager=>create_by_http_destination( lo_destination ).
> lo_client_proxy = /iwbep/cl_cp_factory_remote=>create_v4_remote_proxy(
>   EXPORTING
>      is_proxy_model_key       = VALUE #( repository_id       = 'DEFAULT'
>                                          proxy_model_id      = 'BUSINESS_USER'
>                                          proxy_model_version = '0001' )
>     io_http_client             = lo_http_client
>     iv_relative_service_root   = '<service_root>' ).
> 
> ASSERT lo_http_client IS BOUND.
> 
> 
> * Prepare business data
> ls_business_data = VALUE #(
>           id          = '11112222333344445555666677778888'
>           first_name  = 'FirstName'
>           last_name   = 'LastName'
>           phone       = 'Phone'
>           email       = 'Email'
>           address     = 'Address' ).
> 
> " Navigate to the resource and create a request for the create operation
> lo_request = lo_client_proxy->create_resource_for_entity_set( 'USERS' )->create_request_for_create( ).
> 
> " Set the business data for the created entity
> lo_request->set_business_data( ls_business_data ).
> 
> " Execute the request
> lo_response = lo_request->execute( ).
> 
> " Get the after image
> *lo_response->get_business_data( IMPORTING es_business_data = ls_business_data ).
> 
> CATCH /iwbep/cx_cp_remote INTO DATA(lx_remote).
> " Handle remote Exception
> " It contains details about the problems of your http(s) connection
> 
> 
> CATCH /iwbep/cx_gateway INTO DATA(lx_gateway).
> " Handle Exception
> 
> CATCH cx_web_http_client_error INTO DATA(lx_web_http_client_error).
> " Handle Exception
> RAISE SHORTDUMP lx_web_http_client_error.
> 
> ENDTRY.
> ```

> ### Note:  
> We recommend to retrieve the correct destination reference based on the communication scenario and a customer-defined property as described in [Service Consumption via Communication Arrangements](service-consumption-via-communication-arrangements-86aece6.md).



<a name="loio418787f81805485f993ce21d15152092__postreq_cq3_ctx_kzb"/>

## Next Steps

To test your outbound call, you have to provide a configuration for the outbound service you want to call in your code.

Create a communication system and communication arrangement for the communication scenario in the Communication Systems and Communication Arrangements apps and maintain the required data.

These tasks are performed by the administrator. For more information, see [Set Up OData Communication](set-up-odata-communication-28db688.md).
