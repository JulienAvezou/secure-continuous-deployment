# secure-continuous-deployment
Notes from DevSecOps ch.9 Secure Continuous Deployment &amp; DAST

Common practice is SSH Port should only be open to a list of whitelisted IP addresses
However SSH in general circumvents aws authentication by accessing server directly
Even better practice is to access EC2 via aws authentication, and then authorization based on policies configured for the user, and close port 22 so SSH is not possible 
-> AWS Systems manager (SSM): enabled secure ops at scale via SSM Agents

To setup SSM:
1. SSM Agent installed on EC2 instance
By default on many EC2 it is installed
<img width="848" alt="Capture d’écran 2024-06-07 à 17 49 34" src="https://github.com/JulienAvezou/secure-continuous-deployment/assets/62488871/a91957ef-399d-4ecf-8286-6a4504469a17">

2. Create role and attach SSM Role to EC2 Instance
<img width="1049" alt="Capture d’écran 2024-06-07 à 17 56 57" src="https://github.com/JulienAvezou/secure-continuous-deployment/assets/62488871/d3fe9cf5-a142-4315-8e9c-f63b8fcb9cfa">
<img width="562" alt="Capture d’écran 2024-06-07 à 17 58 15" src="https://github.com/JulienAvezou/secure-continuous-deployment/assets/62488871/7b84d279-0b68-4e25-9ff3-6f645433bb70">

3. Add step in the pipeline to send cmd with SSM
<img width="1055" alt="Capture d’écran 2024-06-07 à 18 39 34" src="https://github.com/JulienAvezou/secure-continuous-deployment/assets/62488871/53903af3-66ed-4098-87f9-689a57a01d22">

4. Ensure that user running the pipeline has permissions to run SSM cmd
<img width="579" alt="Capture d’écran 2024-06-07 à 18 28 33" src="https://github.com/JulienAvezou/secure-continuous-deployment/assets/62488871/92553bce-27cc-4af3-9f67-238ec90787b7">
<img width="789" alt="Capture d’écran 2024-06-07 à 18 42 34" src="https://github.com/JulienAvezou/secure-continuous-deployment/assets/62488871/f81977dc-a7a6-442a-8b74-da714161879d">
