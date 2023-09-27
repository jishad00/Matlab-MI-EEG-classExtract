close all; clear, clc
%% load data
subjectindex = 1; % Select the subject index out of the nine subjects
    subE = strcat(sprintf('A0%dE.mat',subjectindex));
    subT = strcat(sprintf('A0%dT.mat',subjectindex));
    AE1 = load(subE);
    AT1 = load(subT);
    %% Design filter
    Ap = 0.1;   %Maximum Passband ripple
    Aa = 60;    %Minimum stopband attenuation
    fp1 = 8;  %Lower passband frequency
    fp2 = 30; %Upper passband frequency
    fa1 = 7;  %Lower stopband frequency
    fa2 = 31; %Upper stopband frequency
    fs = 250;  %Sampling frequency

    d = designfilt('bandpassfir','PassbandFrequency1',fp1, ...
        'PassbandFrequency2',fp2, 'StopbandFrequency1',fa1, ...
        'StopbandFrequency2',fa2, 'SampleRate',fs, ...
        'PassbandRipple',Ap,'StopbandAttenuation1',Aa, 'StopbandAttenuation2',Aa,...
        'DesignMethod','kaiserwin');
    %% Subject 1 filterd data
    ch = 22;
    trT = length(AT1.data);
    trE = length(AE1.data);
    % Filtered signal for A01T
    for r = trT-5:trT
        for i = 1:ch
            FAT1.data{1, r-(trT-6)}.X(:,i) = filtfilt(d, AT1.data{1, r}.X(:,i));
        end
        FAT1.data{1,r-(trT-6)}.trial = AT1.data{1, r}.trial;
        FAT1.data{1,r-(trT-6)}.y = AT1.data{1, r}.y;
        FAT1.data{1,r-(trT-6)}.fs = AT1.data{1, r}.fs;
        FAT1.data{1,r-(trT-6)}.classes = AT1.data{1, r}.classes;
        FAT1.data{1,r-(trT-6)}.artifacts = AT1.data{1, r}.artifacts;
        FAT1.data{1,r-(trT-6)}.gender = AT1.data{1, r}.gender;
        FAT1.data{1,r-(trT-6)}.age = AT1.data{1, r}.age;
    end

    % Filtered signal for A01E
    for r = trE-5:trE
        for i = 1:ch
            FAE1.data{1, r-(trE-6)}.X(:,i) = filtfilt(d, AE1.data{1, r}.X(:,i));
        end
        FAE1.data{1,r-(trE-6)}.trial = AE1.data{1, r}.trial;
        FAE1.data{1,r-(trE-6)}.y = AE1.data{1, r}.y;
        FAE1.data{1,r-(trE-6)}.fs = AE1.data{1, r}.fs;
        FAE1.data{1,r-(trE-6)}.classes = AE1.data{1, r}.classes;
        FAE1.data{1,r-(trE-6)}.artifacts = AE1.data{1, r}.artifacts;
        FAE1.data{1,r-(trE-6)}.gender = AE1.data{1, r}.gender;
        FAE1.data{1,r-(trE-6)}.age = AE1.data{1, r}.age;
    end
    %% Subject data combined to single file
    FA1 = FAT1;
    for i = 1:6
        FA1.data{1, 6+i} = FAE1.data{1, i};
    end
    %% Class extraction from Subject EEG data
    run = 12;
    trl = 48;
    ch = 22;
    sampfreq = 250;
    delay = 3*sampfreq; % delay includes the time for beep, fixation cross and cue; refer timing scheme
    duration = 3*sampfreq; % 3 second task specific EEG
    % extracting class data
    n = 1;
    m = 1;
    j = 1;
    k = 1;
    for r = 1:run
        for i = 1:trl
            x1 = FA1.data{1, r}.y(i,1); %class
            x2 = FA1.data{1, r}.trial(i,1); %trial sample start point
            if x1 == 1
                CLS1.data{n,x1} = FA1.data{1, r}.X(x2+delay:x2+delay+duration-1,:);
                n = n+1;
            end
            if x1 == 2
                CLS1.data{m,x1} = FA1.data{1, r}.X(x2+delay:x2+delay+duration-1,:);
                m = m+1;
            end
            if x1 == 3
                CLS1.data{j,x1} = FA1.data{1, r}.X(x2+delay:x2+delay+duration-1,:);
                j = j+1;
            end
            if x1 == 4
                CLS1.data{k,x1} = FA1.data{1, r}.X(x2+delay:x2+delay+duration-1,:);
                k = k+1;
            end

        end
    end
