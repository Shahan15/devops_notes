Issue: Initial image built was 2.7Gb and took minutes to build - realised that the image was still holding onto the compilers downloaded to compile Go. 

Solution: Introduced a third stage - this simply copied the Compiled Go code from the Stage 2 (builder) - this contained the frontend assets as well as the compiled Go code. 
![[Screenshot 2026-06-18 at 00.02.08.png]]