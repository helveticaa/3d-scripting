import maya.cmds as mc

# README: input your own info for these three variables.
substancePrefix = 'MimicLowPolyUVs_'
filePath = 'C:\Users\zachw\Downloads\Mimic\Textures'
fileType = ".png"

allMats = mc.ls(materials=True)
numMats = len(allMats)

# mapTypes: string BaseColor, Metallic, Roughness, Normal
def InputMap(mapType):
    # Create texture file node network
    curTextureNode = mc.shadingNode('file', asTexture=True, isColorManaged=True)
    curPlaceNode = mc.shadingNode('place2dTexture', asUtility=True)
    mc.connectAttr(curPlaceNode+'.coverage', curTextureNode+'.coverage')
    mc.connectAttr(curPlaceNode+'.translateFrame', curTextureNode+'.translateFrame')
    mc.connectAttr(curPlaceNode+'.rotateFrame', curTextureNode+'.rotateFrame')
    mc.connectAttr(curPlaceNode+'.mirrorU', curTextureNode+'.mirrorU')
    mc.connectAttr(curPlaceNode+'.mirrorV', curTextureNode+'.mirrorV')
    mc.connectAttr(curPlaceNode+'.stagger', curTextureNode+'.stagger')
    mc.connectAttr(curPlaceNode+'.wrapU', curTextureNode+'.wrapU')
    mc.connectAttr(curPlaceNode+'.wrapV', curTextureNode+'.wrapV')
    mc.connectAttr(curPlaceNode+'.repeatUV', curTextureNode+'.repeatUV')
    mc.connectAttr(curPlaceNode+'.offset', curTextureNode+'.offset')
    mc.connectAttr(curPlaceNode+'.rotateUV', curTextureNode+'.rotateUV')
    mc.connectAttr(curPlaceNode+'.noiseUV', curTextureNode+'.noiseUV')
    mc.connectAttr(curPlaceNode+'.vertexUvOne', curTextureNode+'.vertexUvOne')
    mc.connectAttr(curPlaceNode+'.vertexUvTwo', curTextureNode+'.vertexUvTwo')
    mc.connectAttr(curPlaceNode+'.vertexUvThree', curTextureNode+'.vertexUvThree')
    mc.connectAttr(curPlaceNode+'.vertexCameraOne', curTextureNode+'.vertexCameraOne')
    mc.connectAttr(curPlaceNode+'.outUV', curTextureNode+'.uv')
    mc.connectAttr(curPlaceNode+'.outUvFilterSize', curTextureNode+'.uvFilterSize')
    # connects texture file network to material
    if mapType == 'BaseColor':
        mc.connectAttr(curTextureNode+'.outColor', matName+'.baseColor', f=True)
        mc.setAttr(curTextureNode+'.fileTextureName', filePath + '\\' + substancePrefix + matName +"_BaseColor" + fileType,
                   type='string')
        mc.setAttr(curTextureNode+'.colorSpace', 'sRGB', type='string')
        mc.setAttr(curTextureNode+'.alphaIsLuminance', False)
    if mapType == 'Metallic':
        mc.connectAttr(curTextureNode + '.outAlpha', matName + '.metalness', f=True)
        mc.setAttr(curTextureNode + '.fileTextureName', filePath + '\\' + substancePrefix + matName + "_Metallic" + fileType,
                   type='string')
        mc.setAttr(curTextureNode + '.colorSpace', 'Raw', type='string')
        mc.setAttr(curTextureNode + '.alphaIsLuminance', True)
    if mapType == 'Roughness':
        mc.connectAttr(curTextureNode + '.outAlpha', matName + '.specularRoughness', f=True)
        mc.setAttr(curTextureNode + '.fileTextureName', filePath + '\\' + substancePrefix + matName + "_Roughness" + fileType,
                   type='string')
        mc.setAttr(curTextureNode + '.colorSpace', 'Raw', type='string')
        mc.setAttr(curTextureNode + '.alphaIsLuminance', True)
    if mapType == 'Normal':
        curBumpNode = mc.shadingNode('bump2d', asUtility=True)
        mc.connectAttr(curBumpNode + '.outNormal', matName + '.normalCamera', f=True)
        mc.connectAttr(curTextureNode + '.outAlpha', curBumpNode + '.bumpValue', f=True)
        mc.setAttr(curBumpNode + '.bumpInterp', 1)
        mc.setAttr(curTextureNode + '.fileTextureName', filePath + '\\' + substancePrefix + matName + "_Normal" + fileType,
                   type='string')
        mc.setAttr(curTextureNode + '.colorSpace', 'Raw', type='string')
        mc.setAttr(curTextureNode + '.alphaIsLuminance', False)


for i in range(0, numMats):
    matName = allMats[i]
    if matName == 'lambert1' or matName == 'standardSurface1' or matName == 'particleCloud1':
        continue
    else:
        InputMap('BaseColor')
        InputMap('Metallic')
        InputMap('Roughness')
        InputMap('Normal')
