# PhysioNet Challenge 2016: �S���̐���E�ُ핪��


���̃X�N���v�g�́A�g�ݍ��݋@�B�w�K�A�v���J���̂��߂̈�A�̃��[�N�t���[�A��̓I�ɂ̓f�[�^�̓ǂݍ��݁A�������o�A�e��A���S���Y���̌����A���f���̃`���[�j���O�A�����ăv���g�^�C�v�z�z�܂ł��Љ�܂��B���ɂ����ł́A�댯�ȐS���a�̃��X�N�����銳�҂�f�@�����ËƖ��ŉ��p�\�ŁA�n���Տ���ւ̈ˑ��y���ɂȂ���A�S����"����"��"�ُ�"�𕪗ނ���A���S���Y�����J�����܂��B




**���ӁF���̃X�N���v�g�̓Z�N�V�������ɌʂɎ��s���Ă������Ƃ�z�肵�Ă��܂��B**�M���A�i���C�U�╪�ފw�K��Ȃǂ̃A�v���̎g�p���Ӑ}���Ă��邽�߂ł��B




Copyright 2019-2020 The MathWorks, Inc.




���}�́A�A�v���̃v���g�^�C�v�̊T�σX�N���[���V���b�g�ł��B




![image_0.png](HeartSoundClassification_LiveScript_JP_images/image_0.png)




�����ł� [PhysioNet challenge of 2016](https://physionet.org/challenge/) �Œ񋟂����3000�ȏ�̐���E�ُ�̐S���^���f�[�^���g���܂��B�����̘^���f�[�^�͐S���v�ɂ��4�ӏ��i�����A�x�A�O��فA�m�X�فj�̈ʒu�ŋL�^����Ă��܂��B




�܂��f�[�^���������܂��B�ŏ��ɂ��̃X�N���v�g�����s����ۂ́A���̃X�e�b�v�ŁAPhysioNet�̃E�F�u�T�C�g����f�[�^���_�E�����[�h���܂��B���� "Data" �f�B���N�g��������ꍇ�͂��̃X�e�b�v�̓X�L�b�v����܂��B���邢�́A�������ۂ̓������o�����⃂�f���̊w�K�i�ǂ�������s�ɐ���������܂��j���s��Ȃ��ꍇ�A�w�K�ƕ]���p�̃f�[�^�Z�b�g��p�ӂ���K�v�͂���܂���B���̏ꍇ�͑���ɁAzip�t�@�C����W�J���āA.mat�t�@�C�����炠�炩���ߒ��o���������ʂ�ǂݍ��݁A���ފw�K��Ń��f�����w�K�����܂��B




***Note***: �C���^�[�l�b�g�̐ڑ��󋵂ɂ���Ď��Ԃ�������ꍇ������܂�


```matlab
getTrainingData = 0; % option to skip downloading training data (may take long time, 185 MB)
if ~exist('training.zip') && getTrainingData%#ok 
    % fetch training data from physionet site. 
    % NOTE: unless you plan to execute the feature extraction, don't worry if there is an error here,
    %       we only need access to the training set to run the feature extraction 
    try
        training_url = 'http://www.physionet.org/physiobank/database/challenge/2016/training.zip';
        websave('training.zip', training_url);
    catch
        warning("Failed to access heart sound training data on physionet.org - check your internet connection or whether path %s needs updating",training_url)
    end
    
    unzip('training.zip', 'Data\training')
end

if ~exist('validation.zip')%#ok 
   % you need the validation data only for running the prototype app
   try
       validation_url = 'http://www.physionet.org/physiobank/database/challenge/2016/validation.zip';
       websave('validation.zip', validation_url);
   catch
       warning("Failed to access heart sound validation data on physionet.org - check whether path %s needs updating", validation_url)
   end
   unzip('validation.zip','Data\');
end

% make sure we have copies of the two example files in the main directory
if exist('Data\validation')%#ok
    copyfile 'Data\validation\a0001.wav';
    copyfile 'Data\validation\a0011.wav';
end
```


���݂̃t�H���_�[�ƃT�u�t�H���_�[���p�X�Ƃ��ĉ����A�X�N���v�g���A�T�u�f�B���N�g���@"Data" �Ɋi�[�����^���f�[�^�ƁA"HelperFunctions"�ɕۑ����ꂽMATLAB�֐��e��փA�N�Z�X�ł���悤�ɂ��܂��B


```matlab
addpath(genpath(pwd));
addpath('.\HelperFunctions\');
```


�{�f���̊T�v�́A�T�^�I�ȋ@�B�w�K���[�N�t���[��4�̃t�F�[�Y��z�肵�č\������Ă��܂��F



   1.  �f�[�^�ւ̃A�N�Z�X�Ɖ�� 
   1.  �f�[�^�̑O���� 
   1.  �\�����f���̍쐬 
   1.  ���f���̃V�X�e���ւ̓��� 



���}�́A���[�N�t���[�̊e�t�F�[�Y�Ŋ��p����Toolbox�������Ă��܂��B




![image_1.png ](HeartSoundClassification_LiveScript_JP_images/image_1.png )


![image_2.png](HeartSoundClassification_LiveScript_JP_images/image_2.png)
# �ُ�ȐS�����Đ�����ƁH


��͑Ώۂ̓�����c�����邽�߂ɁA�S���M���̉����Đ����Ă݂܂��BMATLAB�̓I�[�f�B�I�M���̍Đ��@�\�������Ă��܂��B���̗�ł́A����ƈُ�̐S���T���v�����A�f�[�^�Z�b�g���烁�C���̃f�B���N�g���ɃR�s�[���܂��B


```matlab
[PCG_abnormal, fs] = audioread('a0001.wav');
p_abnormal = audioplayer(PCG_abnormal, fs);
play(p_abnormal, [1 (get(p_abnormal, 'SampleRate') * 3)]);

% Plot the sound waveform
plot(PCG_abnormal(1:fs*3))
```

![figure_0.png](HeartSoundClassification_LiveScript_JP_images/figure_0.png)

# ����ȐS���̉��́H
```matlab
[PCG_normal, fs] = audioread('a0011.wav');
p_normal = audioplayer(PCG_normal, fs);
play(p_normal, [1 (get(p_normal, 'SampleRate') * 3)]);

% Plot the sound waveform
plot(PCG_normal(1:fs*3))
```

![figure_1.png](HeartSoundClassification_LiveScript_JP_images/figure_1.png)

![image_3.png](HeartSoundClassification_LiveScript_JP_images/image_3.png)
# ���g���̈�ł͐M���͂ǂ�������H


���ފ�Ŕ��ʂ��邱���̐M���̏ڍׂ�c�����邽�߂ɁA���g���������ϑ����Ă݂܂��傤�B������̐M���̃p���[�X�y�N�g����]���E��r����ɂ́AMATLAB�� [Signal Analyzer](https://www.mathworks.com/help/signal/ug/getting-started-with-signal-analyzer-app.html) �A�v�����g�p�ł��܂��B


```matlab
signalAnalyzer(PCG_abnormal, PCG_normal)
```


�A�v�����N������ƁA��̃p�l���ɂ��ꂼ��̐M�����\������i����̃O���b�h�{�^�����g���܂��j�A�e�g�`�̉��ɁA�X�y�N�g������������܂��i�X�y�N�g���{�^���������j�B�ُ퉹�ɂ����ẮA0.2���W�A���t�߂ɃX�p�C�N�������̂ɑ΂��āA���퉹��y���t�߂ɐ������W�����Ă��܂��B




![image_4.png](HeartSoundClassification_LiveScript_JP_images/image_4.png)


![image_5.png](HeartSoundClassification_LiveScript_JP_images/image_5.png)
# �f�[�^�ǂݍ��݂̏���


�������ɘ^���f�[�^��ǂݍ��ލہA��K�̓f�[�^�������K�v����������A�f�[�^�t�@�C���������̃t�H���_�ɕ��U���Ă���ꍇ�́A[fileDatastore](https://www.mathworks.com/help/matlab/ref/filedatastore.html) ���g�p����ƕ֗��ł��Bread�֐��ł͑���̈قȂ�t�@�C���t�H�[�}�b�g�ւ̃A�N�Z�X���\�ł����A�ǂݍ��݂ɂ͑����̃J�X�^�}�C�Y���K�v�ɂȂ邱�Ƃ�����܂��B


```matlab
training_fds = fileDatastore(fullfile(pwd, 'Data', 'training'), 'ReadFcn', @importAudioFile, 'FileExtensions', '.wav', 'IncludeSubfolders', 1);
```
\matlabheading{![image_6.png](HeartSoundClassification_LiveScript_JP_images/image_6.png)}
# �t�@�C�����ƃ��x���̂����e�[�u���̍쐬


"���x��"�i���邢�́A"�O�����h�g�D���[�X"�j�́A�e�f�[�^�Z�b�g�̐^�̃J�e�S���̂��ƂŁA���̕��ޏ����ɓK�����@�B�w�K��K�p���邽�߂ɏd�v�ł��B�����Ŏg�p����f�[�^�Z�b�g�́A�w�K�p�ƕ]���p�̃f�[�^�̕ۑ����ꂽ�e�T�u�t�H���_����PREFERENCE �t�@�C���ɂ���A�ړI�̃I�[�f�B�I�t�@�C���i�^���f�[�^�j�ƍ��v�������x�����������܂��B���̃Z�N�V�����ł́A�����PREFERENCE.csv�t�@�C����ǂݍ��݁A�t�@�C�����ƁA���x�������������e�[�u�����쐬���܂��B���̃X�e�b�v�́A���̃X�e�b�v�̓����ʒ��o���K�v�ȏꍇ�ɂ̂ݎ��s����K�v������܂��B


```matlab
data_dir = fullfile(pwd, 'Data', 'training');
folder_list = dir([data_dir filesep 'training*']);

reference_table = table();

for ifolder = 1:length(folder_list)
    disp(['Processing files from folder: ' folder_list(ifolder).name])
    current_folder = [data_dir filesep folder_list(ifolder).name];
    
    % Import ground truth labels (1, -1) from reference. 1 = Normal, -1 = Abnormal
    reference_table = [reference_table; importReferencefile([current_folder filesep 'REFERENCE.csv'])];
end
```
```
Processing files from folder: training-a
Processing files from folder: training-b
Processing files from folder: training-c
Processing files from folder: training-d
Processing files from folder: training-e
Processing files from folder: training-f
```
![image_7.png](HeartSoundClassification_LiveScript_JP_images/image_7.png)
# ���ۂ̐S���M������̓����ʒ��o


���ɁA���f�[�^����̓������o���s���܂��B���ۂ̐S���M����������𒊏o���邽�߂ɁAMATLAB�Ŏg�p�\�ȓ��v����ѐM�������֐���p���܂��B�ȉ��̃Z�N�V�����ł́A�e�X�̘^������28�̓����𒊏o���A�e�^���f�[�^��5�b�Ԃ̐S�����Ƃɕ������܂��B




��3000�̘^���f�[�^�̑O�����ɂ́A�ȉ��̃R�[�h��Parallel Computing Toolbox�ŕ��񏈗����s�����Ƃ��Ă��A���΂炭���Ԃ�������܂��B�҂����Ԃ�������邽�߂ɁA�{�f���̃f�t�H���g�ݒ�ł́A���炩���ߒ��o���ꂽ�����ʂ��AFeature Table����ǂݍ��ޗl�ɂ��Ă��܂��B


```matlab
if ~exist('FeatureTable.mat')%#ok 
    % Window length for feature extraction in seconds
    win_len = 5;
    
    % Specify the overlap between adjacent windows for feature extraction in percentage
    win_overlap = 0;
    
    % Initialize feature table to accumulate observations
    feature_table = table();
    
    % Use Parallel Computing Toobox to speed up feature extraction by distributing computation across available processors
    
    % Create partitions of the fileDatastore object based on the number of processors
    n_parts = numpartitions(training_fds, gcp);
    
    % Distribute computation across available processors by using parfor
    parfor ipart = 1:n_parts
        % Get partition ipart of the datastore.
        subds = partition(training_fds, n_parts, ipart);
        
        % Extract features for the sub datastore
        feature_table = [feature_table; extractFeatures(subds, win_len, win_overlap, reference_table)];
        
        % Display progress
        disp(['Part ' num2str(ipart) ' done.'])
    end
    save('FeatureTable', 'feature_table');
else % simply load the precomputed features
    load('FeatureTable.mat');
end

% Take a look at the feature table
disp(feature_table(1:5,:))
```
```
     meanValue     medianValue    standardDeviation    meanAbsoluteDeviation    quantile25    quantile75    signalIQR    sampleSkewness    sampleKurtosis    signalEntropy    spectralEntropy    dominantFrequencyValue    dominantFrequencyMagnitude    dominantFrequencyRatio    MFCC1     MFCC2     MFCC3       MFCC4       MFCC5       MFCC6      MFCC7      MFCC8       MFCC9      MFCC10     MFCC11      MFCC12     MFCC13       class   
    ___________    ___________    _________________    _____________________    __________    __________    _________    ______________    ______________    _____________    _______________    ______________________    __________________________    ______________________    ______    ______    ______    _________    ________    _______    _______    ________    ________    ______    ________    ________    _______    __________

    -2.7121e-05     0.00015259         0.02033                0.01228           -0.0083771    0.0082092     0.016586         1.4484            21.147           -2.7659           0.28682                17.098                     0.066932                    0.22436            88.196    7.3405    6.4674    -0.051239     -2.5149     -3.143    -1.9638    -0.11315    -0.28488    1.6218    -0.53338     -1.6926    -2.0239    'Abnormal'
    -4.3304e-06     6.1035e-05        0.021358               0.012943           -0.0079041    0.0081482     0.016052        0.59825            16.507           -2.7017           0.29779                15.633                     0.051741                    0.16802            88.048    7.9407    6.6784     -0.33812     -1.7421    -4.6783    -2.7332       2.394     0.10001    2.9168     -1.3413    -0.90557    -1.4914    'Abnormal'
     1.6452e-05     0.00036621        0.021588               0.013572           -0.0092163    0.0085297     0.017746          1.039            14.776           -2.6434           0.23184                 26.38                     0.090545                    0.38065            90.012    8.0685    1.5072      -2.2183    -0.55386    -1.3512    -2.2507      1.1322    -0.42672    2.3943      1.5946     -2.0933    -1.3693    'Abnormal'
    -7.8979e-05    -0.00015259        0.019643               0.012688           -0.0090179     0.008606     0.017624        0.78882            13.674            -2.716           0.25299                24.915                     0.065139                     0.4354            87.303    7.4797    7.4607     -0.73843    -0.74028    -4.1818    -2.0782      1.8257       0.865    2.4926    -0.91656    -0.55254    -2.2298    'Abnormal'
     4.4342e-06     0.00048828        0.023276               0.012722           -0.0072021    0.0073853     0.014587         1.2829            21.825           -2.7703           0.27842                30.288                     0.051823                    0.34453            88.171    7.8968    6.8715      0.85403    -0.82052    -5.8922    -2.0241      1.5196    -0.64708     3.923     -0.5634     -1.7582    -0.4827    'Abnormal'
```
![image_8.png](HeartSoundClassification_LiveScript_JP_images/image_8.png)
# �w�K�A��r�A���ފ�̑I�� 


�����ʂ𒊏o������́A�@�B�w�K�̃��[�N�t���[�A���Ȃ킿�A�e��\�����f���̊w�K��Ƃɓ����Ă����܂��B�����ł́A�C���^���N�e�B�u�Ɋw�K�A��r�A���ފ�̑I�����s����A[Classification Learner App](https://www.mathworks.com/help/stats/classificationlearner-app.html) ���g�p���܂��B


```matlab
classificationLearner
```


���[�N�X�y�[�X����A�ϐ��Ƃ��� `feature_table` ��I�����A���f�����؃f�[�^��30% �Ƃ���z�[���h�A�E�g�����I�Ԃ��A��葽���̊w�K�f�[�^���m�ۂ��邽�߂ɁA���������I�����Ă��悢�ł��傤�B




���`��A�ASVM�A����ؓ��̊e���@�Ŋw�K�����܂��B�z�[���h�A�E�g����f�[�^�ɂ����āA�ǂꂪ�ł��������x���o�������ׂ܂��B�܂��A�����s��𒲂ׁA���p�I�Ȋϓ_����A����ȐS���ƈُ�ȐS���Ƃ̌땪�ނ��Ӗ����邱�Ƃ��������܂��B




�����ُ̈퉹���A����ł���ƌ땪�ނ���Ă���A����́A�[���ȐS���a������������Ȃ����҂���f�f����\�������邱�Ƃ��Ӗ����邽�߁A�Տ��f�f�ɂ����ďd��Ȗ��ƂȂ肩�˂܂���B���f���̐��x�����P���邽�߂ɁA�ȉ��̃Z�b�V�����ł́A����Ȃ�œK�����s���Ă����܂��B

![image_9.png](HeartSoundClassification_LiveScript_JP_images/image_9.png)
# �f�[�^���w�K�p�ƃe�X�g�p�ɕ����� 


�����̍œK���̎菇�́A�v���O�����ŏ�������K�v������܂��B�]���āA�O�̃Z�N�V�����ɂ����ĕ��ފw�K��A�v�����Ńf�[�^�𕪊�������ƂƓ��l�ɁA�w�K�f�[�^��30%���e�X�g�p�ɕێ����܂��B[cvpartition](https://www.mathworks.com/help/stats/cvpartition.html) ���g�p���A�w�K�p�ƃe�X�g�p�Ƀf�[�^�𕪊����܂��B�܂��A[grpstats](https://www.mathworks.com/help/stats/grpstats.html) �ɂ��A�e�N���X�Ƃ��Ċϑ����ꂽ�����J�E���g���܂��B


```matlab
rng(1)
% Use 30% of data for training and remaining for testing
split_training_testing = cvpartition(feature_table.class, 'Holdout', 0.3);

% Create a training set
training_set = feature_table(split_training_testing.training, :);

% Create a test set (won't be used until much later)
testing_set = feature_table(split_training_testing.test, :);

grpstats_training = grpstats(training_set, 'class', 'mean');
disp(grpstats_training(:,'GroupCount'))
```
```
                GroupCount
                __________

    Abnormal       2211   
    Normal         6900   
```
![image_10.png](HeartSoundClassification_LiveScript_JP_images/image_10.png)
# �땪�ރR�X�g���ӂ܂������ފ�̊w�K


�f�[�^����"�ُ�"�̊ϑ��̏��Ȃ���⏞���邽�߁A�܂��A�ُ퉹�̌땪�ނ���菭�Ȃ�����l�ɕ��ފ�Ƀo�C�A�X�������邽�߂ɁA"�ُ�"�N���X�ɑ΂��Ă�荂���땪�ރR�X�g��ݒ肷��Acost�֐����g�p���܂��B�����ɁA���f���p�����[�^�̍œK�Ȓl�������邽�߂ɁA[Bayesian Optimization](https://www.mathworks.com/help/stats/bayesian-optimization-workflow.html)��p���āA�n�C�p�[�p�����[�^�̃`���[�j���O���s���܂��B���ފw�K��A�v���ł́A����؂̃A���T���u�����ASVM�̕��ފ���������\�ł��������߁A�����ł̓A���T���u�����g�p���܂��B 


```matlab
% Assign higher cost for misclassification of abnormal heart sounds
C = [0, 20; 1, 0];

% Create a random sub sample (to speed up training) from the training set
%subsample = randi([1 height(training_set)], round(height(training_set)/4), 1);
subsample = 1:height(training_set);

rng(1);

% Create a 5-fold cross-validation set from training data
cvp = cvpartition(length(subsample),'KFold',5);

if ~exist('TrainedEnsembleModel.mat')%#ok
    % perform training only if we don't find a saved model

    % train ensemble of decision trees (random forest)
    disp("Training Ensemble classifier...")
    
    % bayesian optimization parameters (stop after 15 iterations)
    opts = struct('Optimizer','bayesopt','ShowPlots',true,'CVPartition',cvp,...
            'AcquisitionFunctionName','expected-improvement-plus','MaxObjectiveEvaluations',15);    
    trained_model = fitcensemble(training_set(subsample,:),'class','Cost',C,...
        'OptimizeHyperparameters',{'Method','NumLearningCycles','LearnRate'},...
        'HyperparameterOptimizationOptions',opts)

    save('TrainedEnsembleModel', 'trained_model');
else
    % load previously saved model
    load('TrainedEnsembleModel.mat')
end

% Predict class labels for the validation set using trained model
% NOTE: if training ensemble without optimization, need to use trained_model.Trained{idx} to predict
predicted_class = predict(trained_model, testing_set);

conf_mat = confusionmat(testing_set.class, predicted_class);

conf_mat_per = conf_mat*100./sum(conf_mat, 2);

% Visualize model performance in heatmap
labels = {'Abnormal', 'Normal'};
heatmap(labels, labels, conf_mat_per, 'Colormap', winter, 'ColorbarVisible','off');
```

![figure_2.png](HeartSoundClassification_LiveScript_JP_images/figure_2.png)

![image_11.png](HeartSoundClassification_LiveScript_JP_images/image_11.png)
# �ߖT�������͂ɂ������ʂ̑I��


��L���f���̐��x�͔��ɗǍD�ł������A���K�͂ȑg�ݍ��f�o�C�X�ւ̎����ɂ͑傫�����܂��B�]���Ă��̃Z�N�V�����ł́A28�̓����ʂ̂����A�\�����x�̊�^���̑傫�ȓ����ʂ𕔕��I�ɗp�����A���R���p�N�g�ȃ��f���̊w�K���l���܂��B[Neighborhood Component Analysis](https://www.mathworks.com/help/stats/neighborhood-component-analysis.html) (NCA) �́A���o���������̏璷�����ŏ������A���ނ��邽�߂ɂ��L�p�ȏ����������ʂ����𕪕ʂ��邽�߂̎�@�ł��B 


```matlab
runNCA = 1;   % set this to 0 to skip

if ~runNCA && exist('SelectedFeatures.mat')%#ok
    % Load saved array of selected feature indexes
    load('SelectedFeatures.mat')
else % Perform feature selection with neighborhood component analysis
    rng(1)
    mdl = fscnca(table2array(training_set(:,1:27)), ...
        table2array(training_set(:,28)), 'Lambda', 0.005, 'Verbose', 0);
    
    % Select features with weight above 0.1
    selected_feature_indx = find(mdl.FeatureWeights > 0.1);

    % Plot feature weights
    stem(mdl.FeatureWeights,'bo');
    
    save('SelectedFeatures.mat','selected_feature_indx');
end
```

![figure_3.png](HeartSoundClassification_LiveScript_JP_images/figure_3.png)

```matlab
% Display list of selected features
disp(feature_table.Properties.VariableNames(selected_feature_indx))
```
```
  1 �񂩂� 8 ��

    'sampleKurtosis'    'dominantFrequency�c'    'MFCC1'    'MFCC2'    'MFCC3'    'MFCC4'    'MFCC5'    'MFCC6'

  9 �񂩂� 15 ��

    'MFCC7'    'MFCC8'    'MFCC9'    'MFCC10'    'MFCC11'    'MFCC12'    'MFCC13'
```
![image_12.png](HeartSoundClassification_LiveScript_JP_images/image_12.png)
# �I�����ꂽ�����ʂ��g�����w�K


�z�z�p�Ƃ��Ă��R���p�N�g�ȃ��f���ɂ��邽�߂ɑI�����ꂽ�����ʂ������g���ă��f�����w�K�����܂��B�t�@�C���T�C�Y��6MB����4MB�܂ō팸�������Ƃ��m�F�ł��܂��B����ɏ��K�͂ɂ��邽�߂ɁA���̃��f�����������Ƃ��ł��܂��B


```matlab
if ~exist('TrainedEnsembleModel_FeatSel.mat')%#ok
    rng(1)
    opts = struct('Optimizer','bayesopt','ShowPlots',true,'CVPartition',cvp,...
            'AcquisitionFunctionName','expected-improvement-plus','MaxObjectiveEvaluations',15);    
    trained_model_featsel = fitcensemble(training_set(subsample,selected_feature_indx),training_set.class(subsample),'Cost',C,...
        'OptimizeHyperparameters',{'Method','NumLearningCycles','LearnRate'}, 'HyperparameterOptimizationOptions',opts)
    save('TrainedEnsembleModel_FeatSel', 'trained_model_featsel');
else
    load('TrainedEnsembleModel_FeatSel.mat')
end

% Predict class labels for the validation set using trained model
predicted_class_featsel = predict(trained_model_featsel, testing_set(:,selected_feature_indx));

conf_mat_featsel = confusionmat(testing_set.class, predicted_class_featsel);

conf_mat_per_featsel = conf_mat_featsel*100./sum(conf_mat_featsel, 2);

labels = {'Abnormal', 'Normal'};

% Visualize model performance
% probably custom AE version: heatmap(conf_mat_per_featsel, labels, labels, 1,'Colormap', 'red','ShowAllTicks',1,'UseLogColorMap',false,'Colorbar',true);
heatmap(labels,labels,conf_mat_per_featsel, 'Colormap', winter, 'ColorbarVisible','off');
```

![figure_4.png](HeartSoundClassification_LiveScript_JP_images/figure_4.png)

![image_13.png](HeartSoundClassification_LiveScript_JP_images/image_13.png)
# �R�[�h����


�^���M���ƃT���v�����O���g������͂Ƃ��A�S���̕��ރ��x�����o�͂Ƃ���C�R�[�h�𐶐����܂��B���̏����ɂ͐���������܂��B


```matlab
% Save trained model as a compact model for code generation
saveCompactModel(trained_model_featsel,'HeartSoundClassificationModel');

% Alternatively, execute the following auto-generated MATLAB script to generate C code (and mex file, in current directory)
classifyHeartSounds_script
```
```
�R�[�h�̐������������܂���:���|�[�g�̕\��
```
```matlab
copyfile codegen\mex\classifyHeartSounds\classifyHeartSounds_mex.mexw64 HelperFunctions\
```
# �ŏI���f���̌���


�T���v���A�v���ŁA���؃Z�b�g�i"validation"�T�u�t�H���_�j�̉����t�@�C���̈ꕔ���������܂��B�A�v���́A`classifyHeartSounds `�֐���mex�t�@�C�����R�[�����Ă��܂��B


```matlab
plotPredictions
```
```
    'File: '    'a0001'    'Actual: '    'Abnormal'    ' --- Predicted: '    'Abnormal'
    'File: '    'a0002'    'Actual: '    'Abnormal'    ' --- Predicted: '    'Abnormal'
    'File: '    'a0003'    'Actual: '    'Abnormal'    ' --- Predicted: '    'Abnormal'
    'File: '    'a0004'    'Actual: '    'Abnormal'    ' --- Predicted: '    'Normal'
```
