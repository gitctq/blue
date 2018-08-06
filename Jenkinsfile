pipeline
{
  agent {
          label "Windows"
        }
  stages 
      {
       stage('Prepare')
	    {
          steps {
                git branch: 'develop', credentialsId: 'a1d60564-699b-42c8-a313-2982c9a1c678', url: 'git@10.199.104.77:casc/c-sharp.git'
             }
        }
       stage('Build')
	    {
		  steps 
		  {
		   script 
		   {
		      bat 'nuget restore MvcApplicationTest.sln'
		      bat 'nuget install Microsoft.VisualStudio.QualityTools.UnitTestFramework.Updated'
		      Msbuild = tool  'MSBuild Tools 2015'
		      bat (/"${Msbuild}\msbuild.exe" \/P:Configuration=Release \/p:VisualStudioVersion=12.0 MvcApplicationTest.sln && exit %%ERRORLEVEL%% /)
		      
		    }
          }
		}
       stage('Deploy')
        {
		 steps
		  {
		   script
		    {
			  Msbuild = tool  'MSBuild Framework 4.0 64bits'
			  bat (/"${Msbuild}\msbuild.exe" "${WORKSPACE}\MvcApplicationTest\MvcApplicationTest.csproj" \/T:Build;Package \/p:Configuration=RELEASE \/p:OutputPath="obj\RELEASE" \/p:DeployIisAppPath="\/Default Web Site\/namb" \/p:VisualStudioVersion=12.0 /)
			  def DirWorkspace = "${WORKSPACE}\\MvcApplicationTest\\obj\\Release\\_PublishedWebsites\\MvcApplicationTest_Package\\MvcApplicationTest.zip"
			  def ServerDeploy = '10.199.101.204'
			  bat (/call "D:\Program Files (x86)\Jenkins\scripts\deploy_aplicacao_net_cloud.bat" "${DirWorkspace}" "${ServerDeploy}" /)
			}
		  }
		}	   
      }
}