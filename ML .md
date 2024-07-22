#we used this code for ANN part in MATLAB:
#we separated the file based on 3 outputs (Seebeck, Electrical conductivity, Thermal conductivity)
#each output is considered as Y and other input values are considered as X. Then X and Y are converted to transpose matrix and this code is applied.


for i =1:1:10
for N=1:1:25
    R=N;
net= feedforwardnet(R);
net= configure(net,input,target);
[net,tr] = train(net,input,target);
output = net(input);
 e(N)= sum((output-target).^2)/length(output);
  [r,m,b] = regression(target,output);
  q(N) = r; 
  a= 1+4*(i-1);
  U(a,N)= R;
  b= 2+4*(i-1);
  c= 3+4*(i-1);
end
U(b,1:1:25)= e;
U(c,1:1:25)= q;
end


%% to have the best model for particular N value based on R value
g=0;N=18;r=0;
while r<0.92,
net= feedforwardnet(N);
net= configure(net,input,target);
[net,tr] = train(net,input,target);
output = net(input);
 [r,m,b] = regression(target,output);
g=g+1;
if g>200
break
end
R=r;
 ERROR= sum((output-target).^2)/length(output);
end


%% sa = sensitivity analysis
w1= net.IW{1,1};
w2= net.LW{2,1};
sa =w2*w1;


genFunction (net,'C:\...\...\NAME','MatrixOnly','yes');


%% to generate figures
figure, plotfit(target,output);
figure, plotregression(target,output);


# Genetic algorithm used for optimization with Matlab 2018b  
