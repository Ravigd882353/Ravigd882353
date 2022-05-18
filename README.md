
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%---------------------ERRROR Calculation-------------------------------%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

CH_SollPoint  = [CHalpha1,CHalpha2,CHalpha3,CHalpha4] ;
CH_IstPoint = [8.774,10.792,5.840,5.394];

CV_SollPoint = -[CValpha1,CValpha2,CValpha3,CValpha4];
CV_IstPoint = -[8.497,8.520,1.872,1.870];

% CH_Diff= (CH_SollPoint - CH_IstPoint).^2 ;


% 
% TOLERANCE = 0 ;
% % 
% 
k = 1 ;
l=0;
H  = 1;
V = 1;
sumTotal=0;
for k=1:length(CH_SollPoint)
    while   (CH_SollPoint(k) < CH_IstPoint(k))
    
        CH_IstPoint1(k) = CH_IstPoint(k) - 0.01  ;
        CH_IstPoint(k) = CH_IstPoint1(k);
        CH_Diff(k)= (CH_SollPoint(k) - CH_IstPoint(k)).^2 ;
        CV_Diff(k) = (CV_SollPoint(k) - CV_IstPoint(k)).^2 ; 

        HYP_BF(k) = hypot(CH_Diff(k),CV_Diff(k));
%         sumTotal(k=sumTotal+HYP_BF(k);
        ERR (H,V)= round(sum(HYP_BF(k)),5,'significant');

         l= l+1;
          H = H+1;
          V= V+1;

    end
    
   
  ERR(~ERR)  = [] ;
end

