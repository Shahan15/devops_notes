Issue: Initial image built was 2.7Gb and took minutes to build - realised that the image was still holding onto the compilers downloaded to compile Go. 

Solution: Introduced a third stage - this simply copied the Compiled Go code from the Stage 2 (builder) - this contained the frontend assets as well as the compiled Go code. 
![[Screenshot 2026-06-18 at 00.02.08.png]]



Issue: Very long build times of images ~80-150 seconds. 

Solution: Separated go.mod and go.sum into separate layers and introduced cache mounts.


Issue: When i ran a deployment in ECS i would get the following error -`docker push 446276073026.dkr.ecr.eu-west-1.amazonaws.com/memos-ecs:v3.amd`

this is because i was developing on a mac and the images built were made for mac chips i.e. `/arm`. 

Solution: added `platform` in my docker-compose 
![[Screenshot 2026-06-18 at 16.44.02.png]]