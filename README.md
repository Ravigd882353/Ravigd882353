%----------------------------------required parameter of guiding projection length------------------------------------------------&
C_height = 1.25; %camera height in egovehicle
C_offset = 1.4; %camera offset 
C_distance = 8.4; % camera distance from guiding pojection length
D2GP =  7; % guiding projection distance to Headlight(scheinwerfer)
H_height = 0.72;  % Headlight(scheinwerfer) height
H_width = 0.6; % headlight width
L_Start = 0.75; % total width of egovehicle - guiding projection length 
L_Length =  30; % guiding projection length
L_Width = 0.3; %guiding projection width 
SW_total_length= (D2GP+L_Length);
Total_length = (C_distance + L_Length);
Total_width = 2.1;


H_Error = 0.75:0.75:0.75;
V_ErrorT = -1:-1:-1;  V_Error = V_ErrorT' ;

for  i =1:length(H_Error)

     for j =1:length(V_Error)

%-----------------------------------------Projection view from Headlight-------------------------------------------------------------%

xSWH1 = L_Start-H_width ;      ySWH1 =D2GP;
[H_HYSW1,SWHalpha1,SWHbeta1] = triangle(xSWH1,ySWH1);
[V_HYSW1,SWValpha1,SWVbeta1] = triangle(H_height,ySWH1);
xSWH2 = (xSWH1+L_Width) ;      ySWH2 =D2GP;
[H_HYSW2,SWHalpha2,SWHbeta2] = triangle(xSWH2,ySWH2);
[V_HYSW2,SWValpha2,SWVbeta2] = triangle(H_height,ySWH2);
xSWH3 = (xSWH1+L_Width);      ySWH3 =SW_total_length;
[H_HYSW3,SWHalpha3,SWHbeta3] = triangle(xSWH3,ySWH3);
[V_HYSW3,SWValpha3,SWVbeta3] = triangle(H_height,ySWH3);
xSWH4 = L_Start-H_width ;      ySWH4 =SW_total_length;
[H_HYSW4,SWHalpha4,SWHbeta4] = triangle(xSWH4,ySWH4);
[V_HYSW4,SWValpha4,SWVbeta4] = triangle(H_height,ySWH4);
%----------------------------projection view from Camera---------------%
xCH1 = L_Start  ;  yCH1 = C_distance;
[H_HYC1,CHalpha1,CHbeta1] = triangle(xCH1,yCH1);
[HYCV1,CValpha1,CVbeta1] = triangle(C_height,yCH1);
xCH2 = (Total_width) / 2;    yCH2 = C_distance;
[H_HYC2,CHalpha2,CHbeta2] = triangle(xCH2,yCH2);
[HYCV2,CValpha2,CVbeta2] = triangle(C_height,yCH2);
xCH3 = (Total_width) / 2;     yCH3 = Total_length;
[H_HYC3,CHalpha3,CHbeta3] = triangle(xCH3,yCH3);
[HYCV3,CValpha3,CVbeta3] = triangle(C_height,yCH3);
xCH4 = L_Start;     yCH4 = Total_length;        
[H_HYC4,CHalpha4,CHbeta4] = triangle(xCH4,yCH4);
[HYCV4,CValpha4,CVbeta4] = triangle(C_height,yCH4);

%patch([-CHalpha1,-CHalpha2,-CHalpha3,-CHalpha4],[-CValpha1,-CValpha2,-CValpha3,-CValpha4],'k')
%---------------------Mistake calculation of Guiding projection from Headlight vertically-----------------------------------------------------%
%---vertical parameter from scheinwerfer[headlight] ---%
SW_VFalpha1 = SWValpha1- V_Error(j) ;
[V_HYSW_VF1,YSW_VFVP1,SW_VFBeta_angle1] = triVfehler(H_height,SW_VFalpha1);
SW_VFalpha2 = SWValpha2- V_Error(j);
[V_HYSW_VF2,YSW_VFVP2,SW_VFBeta_angle2] = triVfehler(H_height,SW_VFalpha2);
SW_VFalpha3 = SWValpha3- V_Error(j);
[V_HYSW_VF3,YSW_VFVP3,SW_VFBeta_angle3] = triVfehler(H_height,SW_VFalpha3);
SW_VFalpha4 = SWValpha4- V_Error(j) ;
[V_HYSW_VF4,YSW_VFVP4,SW_VFBeta_angle4] = triVfehler(H_height,SW_VFalpha4);
%---Horizontal parameter from scheinwerfer[headlight] FOR VERTICAL ANGLE MOVEMENT---%
xSW_VFH1 =L_Start-H_width ; 
H_HYSW_VF1 = YSW_VFVP1; % hypotenuse of horizontal headlight angle for 1st horizontal point OF Vertical fehler
ySW_VFH1 = sqrt((H_HYSW_VF1.^2)-(xSW_VFH1.^2));
[H_HYSW_VF1,SW_VFHP1,SW_VFHP1_beta] = triangle(xSW_VFH1,ySW_VFH1); 
xSW_VFH2 = xSW_VFH1 + L_Width; 
H_HYSW_VF2 = YSW_VFVP2;
ySW_VFH2 = sqrt((H_HYSW_VF2.^2)-(xSW_VFH2.^2));
[H_HYSW_VF2,SW_VFHP2,SW_VFHP2_beta] = triangle(xSW_VFH2,ySW_VFH2);
xSW_VFH3 = xSW_VFH1 + L_Width;
H_HYSW_VF3 = YSW_VFVP3;
ySW_VFH3 =sqrt((H_HYSW_VF3.^2)-(xSW_VFH3.^2));
[H_HYSW_VF3,SW_VFHP3,SW_VFHP3_beta] = triangle(xSW_VFH3,ySW_VFH3);
xSW_VFH4 = L_Start-H_width; 
H_HYSW_VF4 =YSW_VFVP4;
ySW_VFH4 = sqrt((H_HYSW_VF4.^2)-(xSW_VFH4.^2));
[H_HYSW_VF4,SW_VFHP4,SW_VFHP4_beta] = triangle(xSW_VFH4,ySW_VFH4);
%---------------------Mistake calculation of Guiding projection from Headlight horizontally-----------------------------------------------------%
alphaSW_HFHP1 =  SWHalpha1 + H_Error(i)  ;
[xSW_HFHP1,ySW_HFHP1,betaSW_HFHP1] = triHfehler(H_HYSW1,alphaSW_HFHP1);
[HYSW_HFV1,alpha_HFV1,beta_HFV1] = triangle(H_height,ySW_HFHP1);
alphaSW_HFHP2 =  SWHalpha2 + H_Error(i)   ;
[xSW_HFHP2,ySW_HFHP2,betaSW_HFHP2] = triHfehler(H_HYSW2,alphaSW_HFHP2);
[HYSW_HFV2,alpha_HFV2,beta_HFV2] = triangle(H_height,ySW_HFHP2);
alphaSW_HFHP3 =  SWHalpha3+ H_Error(i)   ;
[xSW_HFHP3,ySW_HFHP3,betaSW_HFHP3] = triHfehler(H_HYSW3,alphaSW_HFHP3);
[HYSW_HFV3,alpha_HFV3,beta_HFV3] = triangle(H_height,ySW_HFHP3);
alphaSW_HFHP4 =  SWHalpha4+ H_Error(i)   ;
[xSW_HFHP4,ySW_HFHP4,betaSW_HFHP4] = triHfehler(H_HYSW4,alphaSW_HFHP4);
[HYSW_HFV4,alpha_HFV4,beta_HFV4] = triangle(H_height,ySW_HFHP4);
% %---------------------Mistake calculation of Guiding projection from Camera -----------------------------------------------------%
%-------------------horizontally calculation for horizontally mistaken guiding projection------------------------------%
XC_HFHP1 = (xSW_HFHP1 + (H_width));
YC_HFHP1 = (ySW_HFHP1 + C_offset);
[HYC_HFHP1,alpha_HFHP1,BETA_HFHP1] = triangle(XC_HFHP1,YC_HFHP1);
[HYC_HFVP1,alpha_HFVP1,beta_HFVP1] = triangle(C_height,YC_HFHP1);
XC_HFHP2 = (xSW_HFHP2+ (H_width));
YC_HFHP2 = (ySW_HFHP2+ C_offset);
[HYC_HFHP2,alpha_HFHP2,BETA_HFHP2] = triangle(XC_HFHP2,YC_HFHP2);
[HYC_HFVP2,alpha_HFVP2,beta_HFVP2] = triangle(C_height, YC_HFHP2);
XC_HFHP3 = (xSW_HFHP3+ (H_width));
YC_HFHP3 = (ySW_HFHP3+ C_offset);
[HYC_HFHP3,alpha_HFHP3,BETA_HFHP3] = triangle(XC_HFHP3,YC_HFHP3);
[HYC_HFVP3,alpha_HFVP3,beta_HFVP3] = triangle(C_height,YC_HFHP3);
XC_HFHP4 = (xSW_HFHP4+ (H_width));
YC_HFHP4 = (ySW_HFHP4+ C_offset);
[HYC_HFHP4,alpha_HFHP4,BETA_HFHP4] = triangle(XC_HFHP4,YC_HFHP4);
[HYC_HFVP4,alpha_HFVP4,beta_HFVP4] = triangle(C_height,YC_HFHP4);
 
%patch([XC_HFHP1,XC_HFHP2,XC_HFHP3,XC_HFHP4],[YC_HFHP1,YC_HFHP2,YC_HFHP3,YC_HFHP4],'r','facealpha',0.3,'Marker','+')

% patch([-alpha_HFHP1,-alpha_-HFHP2,-alpha_HFHP3,-alpha_HFHP4,],[-alpha_HFVP1,-alpha_HFVP2,-alpha_HFVP3,-alpha_HFVP4],'b','facealpha',0.5);
 

%%%%%-------------------------------------------headlight moved vertically by mistake and camera view calculation of mistake--------------------------------%%%%%
XC_VFHP1 = (L_Start(i));
YC_VFHP1 = YSW_VFVP1+C_offset;
[HYC_VFHP1,alpha_VFHP1,beta_VFHP1] = triangle(XC_VFHP1,YC_VFHP1);
[HYC_VFVP1,alpha_VFVP1,beta_VFVP1] = triangle(C_height,YC_VFHP1);
XC_VFHP2 = (Total_width./2);
YC_VFHP2 = YSW_VFVP2+ C_offset;
[HYC_VFHP2,alpha_VFHP2,beta_VFHP2] = triangle(XC_VFHP2,YC_VFHP2);
[HYC_VFVP2,alpha_VFVP2,beta_VFVP2] = triangle(C_height,YC_VFHP1);
XC_VFHP3 = (Total_width./2);
YC_VFHP3 = YSW_VFVP3 +C_offset;
[HYC_VFHP3,alpha_VFHP3,beta_VFHP3] = triangle(XC_VFHP3,YC_VFHP3);
[HYC_VFVP3,alpha_VFVP3,beta_VFVP3] = triangle(C_height,YC_VFHP3);
XC_VFHP4 = (L_Start);
YC_VFHP4 = YSW_VFVP4+C_offset;
[HYC_VFHP4,alpha_VFHP4,beta_VFHP4] = triangle(XC_VFHP4,YC_VFHP4);
[HYC_VFVP4,alpha_VFVP4,beta_VFVP4] = triangle(C_height,YC_VFHP3);
% patch([-alpha_VFHP1,-alpha_VFHP2,-alpha_VFHP3,-alpha_VFHP4,],[-alpha_VFVP1,-alpha_VFVP2,-alpha_VFVP3,-alpha_VFVP4],'b','facealpha',0.3);


%%%%%%%%%%%%%%%%%%%%%%%%%%%-----------------------------------Patch area--------------------------------%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
patch([CHalpha1,CHalpha2,CHalpha3,CHalpha4],[-CValpha1,-CValpha2,-CValpha3,-CValpha4],'k','facealpha',0.4);
patch([alpha_HFHP1,alpha_HFHP2,alpha_HFHP3,alpha_HFHP4] ,[-alpha_HFVP1,-alpha_HFVP2,-alpha_HFVP3,-alpha_HFVP4],'g','facealpha',0.5);
patch([alpha_VFHP1,alpha_VFHP2,alpha_VFHP3,alpha_VFHP4,],[-alpha_VFVP1,-alpha_VFVP2,-alpha_VFVP3,-alpha_VFVP4],'b','facealpha',0.3);





     end 
end
